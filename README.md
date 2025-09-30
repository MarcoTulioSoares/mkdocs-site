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

### Como rodar o MkDocs no Windows

1. Instale o Python:  
   Baixe e instale o Python em https://www.python.org/downloads/windows/

2. Instale o MkDocs e o tema Material:  
   Abra o Prompt de Comando e execute:
   ```
   pip install mkdocs mkdocs-material
   ```

3. (Opcional) Instale plugins extras, se necessário:
   ```
   pip install mkdocs-material-extensions
   ```

4. Inicie o servidor local:
   ```
   mkdocs serve
   ```
   O site estará disponível em http://127.0.0.1:8000

5. Para gerar os arquivos estáticos:
   ```
   mkdocs build
   ```

**Dica:** Execute os comandos na pasta onde está o arquivo `mkdocs.yml`.

### Deploy

O deploy é realizado automaticamente por meio do GitHub Actions. Toda vez que houver um push na branch `main`, a documentação será construída e publicada em GitHub Pages.

O site está disponível em: https://MarcoTulioSoares.github.io/mkdocs-site

## Backlog e contribuições

Consulte [docs/backlog.md](docs/backlog.md) para o backlog genérico e [docs/contribuindo.md](docs/contribuindo.md) para orientações de contribuição.
