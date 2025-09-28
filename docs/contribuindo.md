# Contribuindo

Bem-vinde! Esta seção orienta como colaborar com o backend e com esta documentação.

## Fluxo de trabalho sugerido

1. Abra uma issue descrevendo o problema ou a funcionalidade desejada. Use labels do backlog e vincule-se a itens existentes quando fizer sentido.
2. Crie uma branch a partir de `main` com um nome descritivo, por exemplo:
   - `feature/cadastro-filial`
   - `bugfix/corrige-validacao-ferramenta`
   - `docs/atualiza-endpoints`
3. Faça commits pequenos com mensagens no imperativo (ex.: `Ajusta validacao de filial`).
4. Envie um Pull Request para `main` contendo:
   - descrição das mudanças;
   - referência para a issue relacionada (`Closes #ID`);
   - evidências de testes executados (logs, prints, comandos).
5. Aguarde a revisão, aplique ajustes solicitados e mantenha a branch atualizada com `main` quando necessário.

## Checklist antes de abrir PR

- Executar `./mvnw test` (ou `mvnw.cmd test` no Windows) dentro de `springboot/demo`.
- Rodar `docker compose up --build` localmente quando houver ajustes em infraestrutura.
- Atualizar a documentação em `docs/` sempre que houver mudanças em endpoints ou contratos.
- Garantir que o `mkdocs build` finalize sem erros.

## Padrões de código e estilo

- Utilize Lombok conforme já aplicado às entidades e DTOs, evitando duplicação de getters/setters.
- Prefira lançar `ResponseStatusException` com mensagens claras em validações de negócio.
- Mantenha os controllers enxutos, delegando regras para as classes de serviço.
- Ao adicionar novas entidades, atualize `schema.sql` e revise a modelagem relacional.

## Como sugerir melhorias na documentação

1. Atualize ou crie arquivos em `docs/` utilizando Markdown e seguindo o tom adotado nas seções atuais.
2. Rode `mkdocs serve` localmente para validar a navegação.
3. Inclua capturas de tela ou exemplos de requisições quando relevante.
4. Abra um PR específico para documentação com o label `tipo:doc`.
