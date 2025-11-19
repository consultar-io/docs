---
title: API CRBM
description: API para consultar dados de profissionais e estabelecimentos no Conselho Regional de Biomedicina (CRBM)
keywords: CRBM, Profissional, Estabelecimento, Consulta, API, Brasil
---

# API CRBM

[<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;">](https://god.gw.postman.com/run-collection/49657121-67b8bdd6-d2a3-4670-919d-23be3058fa49?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D49657121-67b8bdd6-d2a3-4670-919d-23be3058fa49%26entityType%3Dcollection%26workspaceId%3Daff38029-3b6a-4292-a751-b410e14cec19)

## Introdução

Esta API permite consultar e buscar informações sobre profissionais e estabelecimentos registrados nos Conselhos Regionais de Biomedicina (CRBM) do Brasil.

## API Consultar CRBM (Consultar pelo CRBM)

Consulta detalhes de um registro específico.

### Endpoint

`GET https://consultar.io/api/v1/crbm/consultar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| `regiao` | Texto | Sim | Região do registro (01 até 06) | `01` |
| `numero_registro` | Texto | Sim | Número do registro (até 7 dígitos, zeros à esquerda são removidos) | `123456` |

### Resposta

| Parâmetro           | Tipo  | Descrição                 | Exemplo      |
| ------------------- | ----- | ------------------------- | ------------ |
| `regiao`            | Texto | Região do registro        | `01`         |
| `numero_registro`   | Texto | Número do registro        | `123456`     |
| `categoria`         | Texto | Categoria do profissional | `BIOMÉDICO`  |
| `nome_razao_social` | Texto | Nome do profissional      | `JOÃO SILVA` |
| `situacao`          | Texto | Situação do registro      | `ATIVO`      |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/crbm/consultar?regiao=01&numero_registro=123456' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

```json
{
  "regiao": "01",
  "numero_registro": "123456",
  "categoria": "BIOMÉDICO",
  "nome_razao_social": "JOÃO SILVA",
  "situacao": "ATIVO"
}
```

#### Exemplo de Resposta de Erro (404)

```json
{
  "error": "NAO_ENCONTRADO",
  "message": "Nenhum registro foi encontrado para os parâmetros informados."
}
```

## API Buscar CRBM (Buscar pelo Nome)

Realiza busca de profissionais pelo nome.

### Endpoint

`GET https://consultar.io/api/v1/crbm/buscar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| nome_razao_social | Texto | Sim | Nome do profissional | `joao silva` |

### Resposta

| Parâmetro         | Tipo  | Descrição                 | Exemplo      |
| ----------------- | ----- | ------------------------- | ------------ |
| regiao            | Texto | Região do registro        | `01`         |
| numero_registro   | Texto | Número do registro        | `123456`     |
| categoria         | Texto | Categoria do profissional | `BIOMÉDICO`  |
| nome_razao_social | Texto | Nome do profissional      | `JOÃO SILVA` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/crbm/buscar?nome_razao_social=joao+silva' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200 OK)

```json
[
  {
    "regiao": "01",
    "numero_registro": "123456",
    "categoria": "BIOMÉDICO",
    "nome_razao_social": "JOÃO SILVA"
  },
  {
    "regiao": "01",
    "numero_registro": "123457",
    "categoria": "BIOMÉDICO",
    "nome_razao_social": "JOÃO DOS SANTOS SILVA"
  }
]
```

#### Exemplo de Resposta de Erro (404 Not Found)

```json
{
  "error": "NAO_ENCONTRADO",
  "message": "Nenhum registro foi encontrado para os parâmetros informados."
}
```

## Códigos de Status HTTP

| Código | Erro (error) | Descrição |
| --- | --- | --- |
| `400` | `REQUISICAO_INVALIDA` | Veja a mensagem de erro (message) para mais detalhes. |
| `403` | `PLANO_INATIVO` | Plano inativo. Faça uma Recarga. |
| `403` | `CREDITOS_INSUFICIENTES` | Créditos insuficientes. Faça uma Recarga. |
| `404` | `NAO_ENCONTRADO` | Registro não encontrado. |
| `500` | `ERRO` | Veja a mensagem de erro (message) para mais detalhes. |
| `500` | `ERRO_INTERNO` | Ocorreu um erro inesperado no nosso sistema. |
| `503` | `SERVICO_INDISPONIVEL` | Veja a mensagem de erro (message) para mais detalhes. |

## Limites e Considerações

- Cada requisição "Consultar CRBM" consome R$ 0,20 dos créditos
- Cada requisição "Buscar CRBM" consome R$ 0,20 dos créditos
- Somente as respostas com os códigos de status `200` e `404` consomem créditos
- Limite máximo de 100 resultados na "Buscar CRBM"
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte
