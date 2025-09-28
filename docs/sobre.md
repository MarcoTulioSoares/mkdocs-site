# Arquitetura e Organização

Esta seção descreve a arquitetura do backend e como o código está estruturado para manter o domínio da loja de construção.

## Camadas principais

- **Controller**: expõe os endpoints REST sob o prefixo `/api`, separados em controllers específicos para filiais, ferramentas e materiais de construção. Cada controller delega a lógica para o respectivo serviço.
- **Service**: concentra as regras de negócio, validação de dados e orquestração das entidades. Os serviços convertem entidades JPA para DTOs e fazem uso de `ResponseStatusException` para sinalizar problemas de validação.
- **Repository**: interfaces JPA que comunicam com o banco MySQL. A configuração `spring.jpa.hibernate.ddl-auto=update` garante que o schema seja sincronizado conforme as entidades evoluem.
- **DTOs e Entidades**: os DTOs expõem apenas os dados necessários para o consumo da API, enquanto as entidades refletem as tabelas físicas (`tb_filial`, `tb_ferramenta` e `tb_material_construcao`).

## Banco de dados

O script `schema.sql` cria três tabelas relacionadas por chaves estrangeiras:

- `tb_filial`: cadastro das filiais com identificador `codigo_filial`.
- `tb_ferramenta`: ferramentas com atributos como `marca`, `valor` e vínculo obrigatório com uma filial.
- `tb_material_construcao`: materiais com dados de `cor`, `matéria-prima` e referência à filial de origem.

As constraints `ON DELETE RESTRICT` evitam exclusão de filiais com itens associados. O carregamento dessas tabelas é garantido durante o boot da aplicação.

## Configurações relevantes

- **Porta**: por padrão, a API sobe em `8089`, podendo ser sobrescrita pela variável `PORT`.
- **Banco de dados**: URLs, usuário e senha são obtidos das variáveis `MYSQLHOST`, `MYSQLPORT`, `MYSQLDATABASE`, `MYSQLUSER` e `MYSQLPASSWORD` (ou seus equivalentes `DB_*`).
- **CORS**: o bean `CorsConfig` libera requisições de `http://localhost:3000`, permitindo o desenvolvimento de front-ends locais sem bloqueios de navegador.

## Fluxo de dados

1. Uma requisição chega a um endpoint `/api/...`.
2. O controller correspondente valida o caminho e delega para o serviço.
3. O serviço aplica regras de negócio (por exemplo, impedir alteração do ID da filial ou exigir vínculo com filial existente) e acessa os repositórios.
4. As entidades retornadas são convertidas em DTOs para envio ao cliente.
5. Em caso de erro, o serviço lança `ResponseStatusException` com status HTTP adequado (400, 404), propagado automaticamente pela camada web.

## Entidades e relacionamentos

- **FilialEntity** possui listas de ferramentas e materiais carregadas com `@OneToMany`, mantendo a consistência do estoque por filial.
- **FerramentaEntity** e **MaterialConstrucaoEntity** utilizam `@ManyToOne` para referenciar a filial e armazenam atributos específicos de cada item.

Essa organização permite adicionar novas categorias de estoque ou integrações externas preservando a separação de responsabilidades e a rastreabilidade de dados.
