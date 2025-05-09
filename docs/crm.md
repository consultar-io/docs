# CRM - Conselho Regional de Medicina

## Introdução

Esta API permite consultar e buscar informações sobre médicos registrados nos
Conselhos Regionais de Medicina (CRM) do Brasil.

## Endpoints

### 1. Consultar

Consulta detalhes de um registro específico.

#### Endpoint

`GET /api/v1/crm/consultar`

#### Requisição

| Parâmetro         | Tipo  | Obrigatório | Descrição                                                          | Exemplo   |
| ----------------- | ----- | ----------- | ------------------------------------------------------------------ | --------- |
| `uf`              | Texto | Sim         | UF do CRM                                                          | `SP`      |
| `numero_registro` | Texto | Sim         | Número do registro (até 7 dígitos, zeros à esquerda são removidos) | `1234567` |

#### Resposta

| Parâmetro           | Tipo  | Descrição                                                                               | Exemplo                                                                      |
| ------------------- | ----- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `uf`                | Texto | UF do CRM                                                                               | `SP`                                                                         |
| `numero_registro`   | Texto | Número do registro                                                                      | `1234567`                                                                    |
| `categoria`         | Texto | Categoria do profissional                                                               | `MÉDICO`                                                                     |
| `nome_razao_social` | Texto | Nome ou razão social do profissional                                                    | `JOÃO DA SILVA`                                                              |
| `situacao`          | Texto | Situação do registro                                                                    | `APOSENTADO`                                                                 |
| `tipo_inscricao`    | Texto | Tipo de inscrição do profissional                                                       | `PRINCIPAL`                                                                  |
| `especialidades`    | Texto | Lista de especialidades com seus respectivos RQE, separadas por vírgula (pode ser null) | `CLÍNICA MÉDICA - RQE Nº 74493, ENDOCRINOLOGIA E METABOLOGIA - RQE Nº 85498` |

#### Erros

| Código HTTP | Erro                     | Mensagem                                                   |
| ----------- | ------------------------ | ---------------------------------------------------------- |
| `400`       | `REQUISICAO_INVALIDA`    |                                                            |
| `403`       | `PLANO_INATIVO`          | `Plano inativo para realizar consultas.`                   |
| `403`       | `CREDITOS_INSUFICIENTES` | `Sem créditos suficientes para consulta.`                  |
| `404`       | `NAO_ENCONTRADO`         | `Nenhum registro encontrado com os parâmetros informados.` |

#### Exemplos

##### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/crm/consultar?uf=sp&numero_registro=1234567' -H 'Authorization: Token <seu-token>'
```

##### Exemplo de Resposta de Sucesso (200)

```json
{
  "uf": "SP",
  "numero_registro": "1234567",
  "categoria": "MÉDICO",
  "nome_razao_social": "JOÃO DA SILVA",
  "situacao": "ATIVO",
  "tipo_inscricao": "PRINCIPAL",
  "especialidades": "CLÍNICA MÉDICA - RQE Nº 74493, ENDOCRINOLOGIA E METABOLOGIA - RQE Nº 85498"
}
```

##### Exemplo de Resposta de Erro (404)

```json
{
  "error": "NAO_ENCONTRADO",
  "message": "Nenhum registro foi encontrado para os parâmetros informados."
}
```

### 2. Buscar por Nome

Realiza busca de médicos por nome.

#### Endpoint

`GET /api/v1/crm/buscar`

#### Requisição

| Parâmetro         | Tipo  | Obrigatório | Descrição                            | Exemplo      |
| ----------------- | ----- | ----------- | ------------------------------------ | ------------ |
| nome_razao_social | Texto | Sim         | Nome ou razão social do profissional | `joao silva` |

#### Resposta

| Parâmetro         | Tipo  | Descrição                            | Exemplo         |
| ----------------- | ----- | ------------------------------------ | --------------- |
| uf                | Texto | UF do CRM                            | `SP`            |
| numero_registro   | Texto | Número do registro                   | `1234567`       |
| categoria         | Texto | Categoria do profissional            | `MÉDICO`        |
| nome_razao_social | Texto | Nome ou razão social do profissional | `JOÃO DA SILVA` |

#### Erros

| Código HTTP | Erro                        | Mensagem                                                   |
| ----------- | --------------------------- | ---------------------------------------------------------- |
| `400`       | `REQUISICAO_INVALIDA`       |                                                            |
| `400`       | `LIMITE_RESULTADO_EXCEDIDO` | `Mais de 100 registros encontrados. Refine sua busca.`     |
| `403`       | `PLANO_INATIVO`             | `Plano inativo para realizar consultas.`                   |
| `403`       | `CREDITOS_INSUFICIENTES`    | `Sem créditos suficientes para consulta.`                  |
| `404`       | `NAO_ENCONTRADO`            | `Nenhum registro encontrado com os parâmetros informados.` |

#### Exemplos

##### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/crm/buscar?nome_razao_social=joao%20silva' -H 'Authorization: Token <seu-token>'
```

##### Exemplo de Resposta de Sucesso (200)

```json
[
  {
    "uf": "SP",
    "numero_registro": "1234567",
    "categoria": "MÉDICO",
    "nome_razao_social": "JOÃO DA SILVA"
  },
  {
    "uf": "SP",
    "numero_registro": "1234568",
    "categoria": "MÉDICO",
    "nome_razao_social": "JOÃO DOS SANTOS SILVA"
  }
]
```

##### Exemplo de Resposta de Erro (404)

```json
{
  "error": "NAO_ENCONTRADO",
  "message": "Nenhum registro foi encontrado para os parâmetros informados."
}
```

## Limites e Considerações

- Cada requisição de "Consultar" consome 1 crédito
- Cada requisição de "Buscar por Nome" consome 1 crédito
- Limite máximo de 100 resultados na "Busca por Nome"
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte
