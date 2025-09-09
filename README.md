# Documentação do Projeto

Este repositório contém a documentação estática do projeto utilizando [MkDocs](https://www.mkdocs.org/) com o tema [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).

## Como usar

### Requisitos

- Python 3.x
- mkdocs e mkdocs-material

### Executar localmente

Instale as dependências:

```bash
pip install mkdocs mkdocs-material
```

Inicie o servidor de desenvolvimento:

```bash
mkdocs serve
```

Acesse em `http://127.0.0.1:8000`.

### Deploy

O deploy é realizado automaticamente por meio do GitHub Actions. Toda vez que houver um push na branch `main`, a documentação será construída e publicada em GitHub Pages.

O site está disponível em: https://MarcoTulioSoares.github.io/mkdocs-site

## Backlog e contribuições

Consulte [docs/backlog.md](docs/backlog.md) para o backlog genérico e [docs/contribuindo.md](docs/contribuindo.md) para orientações de contribuição.
