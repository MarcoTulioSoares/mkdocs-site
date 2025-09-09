# oCntribuindo
Bem-vinde! Esta seção orienta como contribuir com este projeto.

## Fluxo de trabalho

1. Abra uma *issue* descrevendo o problema ou funcionalidade. Use os rótulos apropriados (`tipo:bug`, `tipo:feature`, etc.) e vincule-se a itens do backlog quando houver.
2. Crie uma branch a partir de `main` com um nome descritivo, por exemplo:
   - `feature/nova-funcionalidade`
   - `bug/corrige-link-broken`
   - `doc/ajusta-tutorial`
3. Faça *commits* pequenos e com mensagens claras. Siga o padrão **imperativo** (ex.: `Adiciona página de contato`).
4. Envie um *Pull Request* (PR) para `main`. No PR:
   - Relacione a *issue* correspondente (ex.: "Closes #3").
   - Descreva as mudanças realizadas.
   - Marque revisores.
5. Aguarde a revisão. Ajuste conforme os comentários.
6. Depois de aprovado, o PR será mesclado. A automação de *deploy* publicará o site atualizado.

## Boas práticas

- Mantenha a consistência do estilo e formatação.
- Adicione testes ou exemplos quando possível.
- Atualize a documentação em `docs/` e o `backlog.md` quando necessário.
- Verifique se a pipeline de CI passa antes de solicitar revisão.
