# API REST

Esta referência descreve os endpoints expostos pela API Loja de Construção. Todos os endpoints respondem em JSON e exigem `Content-Type: application/json` para requisições de escrita.

- **Base URL local**: `http://localhost:8089`
- **Prefixo**: `/api`

## Convenções gerais

- Identificadores são inteiros positivos (`Integer`).
- Campos monetários (`valor`) são números decimais (`Double`).
- Relações com filial utilizam o objeto `filial` no formato resumido (`idLancamento`, `nome`).
- Regras de validação utilizam `ResponseStatusException`, retornando status `400 Bad Request` ou `404 Not Found` conforme o caso.

## Filiais (`/api/FILIAL`)

### Estruturas

`FilialResumoDTO`
```json
{
  "idLancamento": 1,
  "nome": "Filial Centro"
}
```

`FilialDetalheDTO`
```json
{
  "idLancamento": 1,
  "nome": "Filial Centro",
  "ferramentas": [ ... ],
  "materiais": [ ... ]
}
```

### Endpoints

| Método | Caminho | Descrição | Sucesso |
|--------|---------|-----------|---------|
| GET | `/api/FILIAL` | Lista todas as filiais cadastradas. | `200 OK` com array de `FilialResumoDTO`. |
| GET | `/api/FILIAL/{id}` | Consulta detalhada com estoque de ferramentas e materiais. | `200 OK` com `FilialDetalheDTO`; `404` se não encontrado. |
| POST | `/api/FILIAL` | Cria uma nova filial. | `201 Created` com `FilialDetalheDTO`; `400` se `nome` ausente ou em branco. |
| PUT | `/api/FILIAL/{id}` | Atualiza o nome da filial. | `200 OK` com `FilialDetalheDTO`; `404` se não encontrado; `400` ao tentar alterar `idLancamento`. |
| DELETE | `/api/FILIAL/{id}` | Remove a filial quando não há dependências. | `204 No Content`; `404` se não encontrado. |

### Exemplo de criação

```http
POST /api/FILIAL HTTP/1.1
Content-Type: application/json

{
  "nome": "Filial Aeroporto"
}
```

Resposta
```json
{
  "idLancamento": 5,
  "nome": "Filial Aeroporto",
  "ferramentas": [],
  "materiais": []
}
```

## Ferramentas (`/api/FERRAMENTA`)

### Estrutura (`FerramentaDTO`)

```json
{
  "codFerramenta": 12,
  "codigoProduto": "FER-001",
  "valor": 199.9,
  "marca": "Bosch",
  "nome": "Furadeira",
  "qtdPacote": 5,
  "filial": {
    "idLancamento": 1,
    "nome": "Filial Centro"
  }
}
```

### Endpoints

| Método | Caminho | Descrição | Sucesso |
|--------|---------|-----------|---------|
| GET | `/api/FERRAMENTA` | Lista todas as ferramentas. | `200 OK` com array de `FerramentaDTO`. |
| GET | `/api/FERRAMENTA/{id}` | Consulta uma ferramenta pelo identificador. | `200 OK` com `FerramentaDTO`; `404` se não encontrado. |
| POST | `/api/FERRAMENTA` | Cria uma nova ferramenta vinculada a uma filial existente. | `201 Created` com `FerramentaDTO`; `400` se filial não informada; `404` se filial inexistente. |
| PUT | `/api/FERRAMENTA/{id}` | Atualiza atributos da ferramenta. | `200 OK`; `404` se não encontrado. |
| DELETE | `/api/FERRAMENTA/{id}` | Remove a ferramenta. | `204 No Content`; `404` se não encontrado. |

### Regras específicas

- O objeto `filial` é obrigatório nas operações de criação e atualização.
- `codigoProduto`, `valor` e `nome` são obrigatórios; ausências resultam em `400 Bad Request`.

## Materiais de construção (`/api/MATERIAL-CONSTRUCAO`)

### Estrutura (`MaterialConstrucaoDTO`)

```json
{
  "codMaterial": 33,
  "codigoProduto": "MAT-003",
  "valor": 59.9,
  "cor": "Cinza",
  "nome": "Cimento CP-II",
  "materiaPrima": "Clínquer",
  "filial": {
    "idLancamento": 1,
    "nome": "Filial Centro"
  }
}
```

### Endpoints

| Método | Caminho | Descrição | Sucesso |
|--------|---------|-----------|---------|
| GET | `/api/MATERIAL-CONSTRUCAO` | Lista todos os materiais cadastrados. | `200 OK` com array de `MaterialConstrucaoDTO`. |
| GET | `/api/MATERIAL-CONSTRUCAO/{id}` | Consulta um material específico. | `200 OK`; `404` se não encontrado. |
| POST | `/api/MATERIAL-CONSTRUCAO` | Cria um novo material vinculado a uma filial existente. | `201 Created`; `400` se filial não informada; `404` se filial inexistente. |
| PUT | `/api/MATERIAL-CONSTRUCAO/{id}` | Atualiza os atributos do material. | `200 OK`; `404` se não encontrado. |
| DELETE | `/api/MATERIAL-CONSTRUCAO/{id}` | Remove o material. | `204 No Content`; `404` se não encontrado. |

### Regras específicas

- `codigoProduto`, `valor` e `nome` são obrigatórios; omissões retornam `400 Bad Request`.
- O campo `filial` deve apontar para uma filial já cadastrada.

## Erros comuns

| Status | Quando ocorre |
|--------|---------------|
| `400 Bad Request` | Dados obrigatórios ausentes, tentativa de alterar ID de filial, filial não informada ao criar itens de estoque. |
| `404 Not Found` | Recurso inexistente (filial, ferramenta ou material). |

## Próximas extensões sugeridas

- Documentar filtros de consulta quando disponíveis (por exemplo, por faixa de preço ou filial).
- Expor documentação OpenAPI gerada automaticamente.
