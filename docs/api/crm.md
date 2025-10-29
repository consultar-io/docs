---
title: API CRM
description: Web Service para consultar dados de profissionais no Conselho Regional de Medicina (CRM)
keywords: API, Web Service, REST, JSON, CRM, Profissional, Consulta, API, Brasil
---

# API CRM

## Introdução

Esta API permite consultar e buscar informações sobre médicos registrados nos Conselhos Regionais de Medicina (CRM) do Brasil.

## API Consultar CRM (Consultar pelo CRM)

Consulta detalhes de um registro específico.

### Endpoint

`GET /api/v1/crm/consultar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| `uf` | Texto | Sim | UF do CRM | `SP` |
| `numero_registro` | Texto | Sim | Número do registro (até 7 dígitos, zeros à esquerda são removidos) | `1234567` |

### Resposta

| Parâmetro | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| `uf` | Texto | UF do CRM | `SP` |
| `numero_registro` | Texto | Número do registro | `1234567` |
| `categoria` | Texto | Categoria do profissional | `MÉDICO` |
| `nome_razao_social` | Texto | Nome ou razão social do profissional | `JOÃO DA SILVA` |
| `situacao` | Texto | Situação do registro | `APOSENTADO` |
| `tipo_inscricao` | Texto | Tipo de inscrição do profissional | `PRINCIPAL` |
| `especialidades` | Texto | Lista de especialidades com seus respectivos RQE, separadas por vírgula (pode ser null) | `CLÍNICA MÉDICA - RQE Nº 74493, ENDOCRINOLOGIA E METABOLOGIA - RQE Nº 85498` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/crm/consultar?uf=sp&numero_registro=1234567' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

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

#### Exemplo de Resposta de Erro (404)

```json
{
  "error": "NAO_ENCONTRADO",
  "message": "Nenhum registro foi encontrado para os parâmetros informados."
}
```

## API Buscar CRM (Buscar pelo Nome)

Realiza busca de médicos pelo nome.

### Endpoint

`GET /api/v1/crm/buscar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| nome_razao_social | Texto | Sim | Nome ou razão social do profissional | `joao silva` |

### Resposta

| Parâmetro | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| uf | Texto | UF do CRM | `SP` |
| numero_registro | Texto | Número do registro | `1234567` |
| categoria | Texto | Categoria do profissional | `MÉDICO` |
| nome_razao_social | Texto | Nome ou razão social do profissional | `JOÃO DA SILVA` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/crm/buscar?nome_razao_social=joao%20silva' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

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

#### Exemplo de Resposta de Erro (404)

```json
{
  "error": "NAO_ENCONTRADO",
  "message": "Nenhum registro foi encontrado para os parâmetros informados."
}
```

## Códigos de Status (HTTP)

| Código | Erro | Descrição |
| --- | --- | --- |
| `400` | `REQUISICAO_INVALIDA` | Requisição inválida. Veja a mensagem para mais detalhes. |
| `403` | `PLANO_INATIVO` | Plano inativo. |
| `403` | `CREDITOS_INSUFICIENTES` | Créditos insuficientes. |
| `404` | `NAO_ENCONTRADO` | Registro não encontrado. |
| `500` | `ERRO` | Aconteceu um erro durante a consulta. Veja a mensagem para mais detalhes. |
| `500` | `ERRO_INTERNO` | Ocorreu um erro inesperado no nosso sistema. |
| `503` | `SERVICO_INDISPONIVEL` | Serviço está temporariamente indisponível. Veja a mensagem para mais detalhes. |

## Limites e Considerações

- Cada requisição "Consultar CRM" consome R$ 0,20 dos créditos
- Cada requisição "Buscar CRM" consome R$ 0,20 dos créditos
- Somente as respostas com os códigos de status `200` e `404` consomem créditos
- Limite máximo de 100 resultados na "Buscar CRM"
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte
