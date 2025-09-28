# Backlog do Projeto

O backlog prioriza as entregas necessárias para manter e evoluir a API da Loja de Construção. Os itens abaixo orientam o desenvolvimento incremental, desde a infraestrutura até funcionalidades específicas de estoque.

## Convenções

- **Labels**: `tipo:bug`, `tipo:feature`, `tipo:task`, `prioridade:alta`, `prioridade:média`, `prioridade:baixa`, `status:em-planejamento`, `status:em-progresso`, `status:em-revisao`, `status:bloqueado`, `status:concluido`.
- **Kanban sugerido**: Backlog → Planejado → Em progresso → Em revisão → Concluído.
- Cada item deve apontar para uma issue e conter critérios de aceitação verificáveis.

## Roadmap inicial

| ID   | Item | Critérios de Aceitação |
|------|------|------------------------|
| BK01 | Pipeline de build e publicação do MkDocs. | Deploy automático no GitHub Pages após merge na `main`. |
| BK02 | Provisionamento local com Docker Compose. | `docker compose up --build` sobe API (`8089`), MySQL (`dbspringboot`) e Adminer (`8080`). |
| BK03 | Configuração de CORS. | Requisições do front-end em `http://localhost:3000` devem ser aceitas sem erros. |

## Histórias de usuário

| ID   | História | Critérios de Aceitação |
|------|----------|------------------------|
| US01 | **Cadastro de filial** — Como gerente regional, quero cadastrar uma filial informando o nome para disponibilizá-la na rede. | `POST /api/FILIAL` com nome válido responde `201 Created` com dados completos; nome vazio gera `400 Bad Request`. |
| US02 | **Atualização de filial** — Como gerente regional, quero atualizar o nome de uma filial existente. | `PUT /api/FILIAL/{id}` com nome válido responde `200 OK`; tentativa de alterar o código gera `400 Bad Request`. |
| US03 | **Listagem de filiais** — Como executivo de expansão, quero listar todas as filiais. | `GET /api/FILIAL` retorna lista (possivelmente vazia) com `idLancamento` e `nome`. |
| US04 | **Consulta detalhada da filial** — Como gerente de loja, quero consultar filiais com estoque completo. | `GET /api/FILIAL/{id}` retorna `ferramentas` e `materiais`; id inexistente responde `404 Not Found`. |
| US05 | **Exclusão de filial** — Como administrador da rede, quero remover filiais encerradas. | `DELETE /api/FILIAL/{id}` devolve `204 No Content` quando remove; inexistente retorna `404`. |
| US06 | **Cadastro de ferramenta** — Como gestor de estoque, quero registrar novas ferramentas vinculadas a uma filial. | `POST /api/FERRAMENTA` exige filial válida; respostas `201` no sucesso, `400` sem filial e `404` para filial inexistente. |
| US07 | **Atualização de ferramenta** — Como gestor de estoque, quero manter dados corretos. | `PUT /api/FERRAMENTA/{id}` atualiza atributos e devolve `200`; id inexistente retorna `404`. |
| US08 | **Listagem de ferramentas** — Como equipe de compras, quero visualizar todas as ferramentas cadastradas. | `GET /api/FERRAMENTA` traz itens com atributos e filial resumida. |
| US09 | **Cadastro de material** — Como comprador corporativo, quero cadastrar novos materiais vinculados a uma filial. | `POST /api/MATERIAL-CONSTRUCAO` exige filial válida; respostas `201`, `400` ou `404` conforme regra. |
| US10 | **Exclusão de material** — Como gestor de estoque, quero remover materiais descontinuados. | `DELETE /api/MATERIAL-CONSTRUCAO/{id}` devolve `204` ao remover; id inexistente retorna `404`. |

## Próximas iniciativas

- Implementar paginação e filtros nos endpoints de listagem.
- Adicionar autenticação/autorização para restringir o acesso à API.
- Disponibilizar documentação OpenAPI gerada automaticamente a partir dos controllers.
