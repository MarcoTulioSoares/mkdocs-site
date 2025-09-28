# Backlog (Genérico)

> Este backlog é um **exemplo inicial** para organizar as tarefas do projeto. Adapte conforme necessário.

## Labels sugeridas

- `tipo:bug`
- `tipo:feature`
- `tipo:task`
- `prioridade:alta`
- `prioridade:média`
- `prioridade:baixa`
- `status:em-planejamento`
- `status:em-progresso`
- `status:em-revisao`
- `status:bloqueado`
- `status:concluido`

## Colunas do Kanban

1. **Backlog** — ideias e tarefas não planejadas
2. **Planejado** — pronto para ser iniciado
3. **Em progresso** — em desenvolvimento
4. **Em revisão** — aguardando revisão
5. **Concluído** — finalizado e testado

## Itens iniciais

- **BK-1**: Configurar MkDocs e tema Material
  _Critérios de aceite_: páginas iniciais prontas e navegação configurada.

- **BK-2**: Pipeline de deploy no GitHub Pages
  _Critérios de aceite_: build automático e site publicado.

- **BK-3**: Criar templates de issues
  _Critérios de aceite_: templates disponíveis para bug, feature e task.

## Backlog de Histórias de Usuário

| ID   | História de Usuário | Critérios de Aceitação |
|------|---------------------|-------------------------|
| US01 | **Cadastro de filial** — Como gerente regional, quero cadastrar uma nova filial informando o nome para disponibilizá-la na rede. | - POST `/api/FILIAL` com nome válido → 201 Created com dados da filial.<br>- Nome ausente/branco → 400 Bad Request e não cria. |
| US02 | **Atualização de filial** — Como gerente regional, quero atualizar o nome de uma filial existente para manter os dados corretos. | - PUT `/api/FILIAL/{id}` com nome válido → 200 OK com dados atualizados.<br>- Alterar código da filial → 400 Bad Request. |
| US03 | **Listagem de filiais** — Como executivo de expansão, quero listar todas as filiais para planejar a cobertura da rede. | - GET `/api/FILIAL` → 200 OK com lista de filiais (código e nome).<br>- Sem filiais → 200 OK com lista vazia. |
| US04 | **Consulta detalhada da filial** — Como gerente de loja, quero consultar os detalhes de uma filial, incluindo ferramentas e materiais, para acompanhar o estoque local. | - GET `/api/FILIAL/{id}` → 200 OK com nome da filial, ferramentas e materiais.<br>- Filial inexistente → 404 Not Found. |
| US05 | **Exclusão de filial** — Como administrador da rede, quero remover uma filial que foi encerrada para manter o cadastro atualizado. | - DELETE `/api/FILIAL/{id}` → 204 No Content.<br>- ID inexistente → 404 Not Found. |
| US06 | **Cadastro de ferramenta** — Como gestor de estoque, quero cadastrar uma nova ferramenta vinculada a uma filial para ampliar o portfólio disponível aos clientes. | - POST `/api/FERRAMENTA` completo → 201 Created com dados + filial resumida.<br>- Sem filial → 400 Bad Request.<br>- Filial inexistente → 404 Not Found. |
| US07 | **Atualização de ferramenta** — Como gestor de estoque, quero atualizar dados de uma ferramenta para manter preços e informações corretos. | - PUT `/api/FERRAMENTA/{id}` válido → 200 OK com dados atualizados.<br>- ID inexistente → 404 Not Found. |
| US08 | **Listagem de ferramentas** — Como equipe de compras, quero listar todas as ferramentas cadastradas para avaliar o portfólio da rede. | - GET `/api/FERRAMENTA` → 200 OK com lista de ferramentas.<br>- Cada item traz atributos + resumo da filial. |
| US09 | **Cadastro de material de construção** — Como comprador corporativo, quero cadastrar um novo material vinculado a uma filial para ampliar as opções de venda. | - POST `/api/MATERIAL-CONSTRUCAO` completo → 201 Created com dados + filial resumida.<br>- Sem filial → 400 Bad Request.<br>- Filial inexistente → 404 Not Found. |
| US10 | **Exclusão de material de construção** — Como gestor de estoque, quero remover um material que saiu de linha para manter o catálogo atualizado. | - DELETE `/api/MATERIAL-CONSTRUCAO/{id}` → 204 No Content.<br>- ID inexistente → 404 Not Found. |
