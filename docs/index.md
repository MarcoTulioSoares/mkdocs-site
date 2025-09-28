# Visão Geral

A **API Loja de Construção** centraliza o cadastro de filiais, ferramentas e materiais de construção que abastecem a rede. Ela foi desenvolvida em Spring Boot e exposta como um conjunto de endpoints REST, consumidos por aplicações internas e painéis de gestão.

## Objetivos do projeto

- Disponibilizar uma API única para o domínio de filiais e seus estoques.
- Garantir consistência de dados entre ferramentas e materiais vinculados a cada filial.
- Facilitar a integração com front-ends hospedados localmente (por exemplo, em `http://localhost:3000`) através de configuração de CORS.

## Principais recursos

- **Gestão de filiais**: CRUD completo, com validações para impedir alteração indevida do identificador da filial.
- **Gestão de estoque**: registro de ferramentas e materiais com vínculo obrigatório a uma filial existente.
- **Relacionamentos ricos**: respostas detalhadas incluem a filial resumida associada a cada item, e os detalhes de uma filial trazem o estoque completo.

## Tecnologias adotadas

- [Spring Boot](https://spring.io/projects/spring-boot) 3.x
- JPA/Hibernate com banco MySQL
- Lombok para redução de código repetitivo nas entidades e DTOs
- Docker Compose para provisionar a API e o banco localmente

## Como executar rapidamente

### Usando Docker Compose

```bash
git clone https://github.com/MarcoTulioSoares/API-LOJA-DE-CONSTRU-O.git
cd API-LOJA-DE-CONSTRU-O
docker compose up --build
```

O serviço `api` será exposto em `http://localhost:8089` e utilizará o banco MySQL interno definido em `docker-compose.yml`.

### Execução local com Maven Wrapper

```bash
git clone https://github.com/MarcoTulioSoares/API-LOJA-DE-CONSTRU-O.git
cd API-LOJA-DE-CONSTRU-O/springboot/demo
./mvnw spring-boot:run
```

Antes de iniciar, configure as variáveis de ambiente `DB_HOST`, `DB_PORT`, `DB_NAME`, `DB_USER` e `DB_PASS`, ou utilize os valores padrão (`localhost`, `3306`, `dbspringboot`, `root`, `root`).

## Próximos passos

- Consulte a página [API REST](api.md) para detalhes dos endpoints.
- Acesse a seção [Arquitetura](sobre.md) para entender a organização do código e da base de dados.
- Verifique o [backlog](backlog.md) para planejar evoluções do produto.
