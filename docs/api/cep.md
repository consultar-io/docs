---
title: API CEP - Consultar CEP e Buscar Endereço
description: Web Service para consultar dados de endereços a partir de um CEP e buscar CEPs a partir de um endereço
keywords: API, Webservice, Web Service, REST, JSON, CEP, Endereço, Correios, Consulta, Busca, Pesquisa, API, Brasil
---

# API CEP (Versão 2)

[<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;">](https://god.gw.postman.com/run-collection/49657121-67b8bdd6-d2a3-4670-919d-23be3058fa49?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D49657121-67b8bdd6-d2a3-4670-919d-23be3058fa49%26entityType%3Dcollection%26workspaceId%3Daff38029-3b6a-4292-a751-b410e14cec19)

## Introdução

Esta API permite consultar os dados de um endereço a partir de um CEP.

## API Consultar CEP (Consultar pelo CEP)

Consulta detalhes de um CEP específico.

### Endpoint

`GET https://consultar.io/api/v2/cep/consultar`

### Requisição

| Parâmetro | Tipo  | Obrigatório | Descrição                   | Exemplo    |
| --------- | ----- | ----------- | --------------------------- | ---------- |
| `cep`     | Texto | Sim         | CEP do endereço (8 dígitos) | `12345678` |

### Resposta

| Campo | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| `cep` | Texto | CEP do endereço sem formatação | `"12345678"` |
| `cep_formatado` | Texto | CEP do endereço com formatação | `"12345-678"` |
| `tipo` | Texto | Tipo de endereço | `"Logradouro"` |
| `caixa_postal` | Booleano | Indicador para caixa postal | `false` |
| `nome` | Texto | Nome do endereço (se aplicável) | `null` |
| `nome_abreviado` | Texto | Nome abreviado do endereço (se aplicável) | `null` |
| `tipo_logradouro` | Texto | Tipo de logradouro (se aplicável) | `"Rua"` |
| `nome_logradouro` | Texto | Nome do logradouro (se aplicável) | `"Exemplo"` |
| `logradouro` | Texto | Logradouro do endereço (se aplicável) | `"Rua Exemplo"` |
| `complemento` | Texto | Complemento do endereço (se aplicável) | `null` |
| `bairro` | Texto | Bairro, distrito ou povoado do endereço (se aplicável) | `"Exemplo"` |
| `bairro_abreviado` | Texto | Bairro abreviado do endereço (se aplicável) | `"Exemplo"` |
| `localidade` | Texto | Município, distrito ou povoado do endereço | `"São Paulo"` |
| `uf` | Texto | Unidade Federativa do endereço | `"SP"` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v2/cep/consultar?cep=12345678' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

```json
{
  "cep": "12345678",
  "cep_formatado": "12345-678",
  "tipo": "Logradouro",
  "caixa_postal": false,
  "nome": null,
  "nome_abreviado": null,
  "tipo_logradouro": "Rua",
  "nome_logradouro": "Exemplo",
  "logradouro": "Rua Exemplo",
  "complemento": null,
  "bairro": "Exemplo",
  "bairro_abreviado": "Exemplo",
  "localidade": "São Paulo",
  "uf": "SP"
}
```

#### Exemplo de Resposta de Erro (404)

```json
{
  "error": "NAO_ENCONTRADO",
  "message": "Nenhum registro foi encontrado para os parâmetros informados."
}
```

### Observações

- O CEP pode ser informado com ou sem hífen

## API Buscar CEP (Buscar pelo Endereço)

Consulta detalhes de um CEP específico.

### Endpoint

`GET https://consultar.io/api/v2/cep/buscar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| `logradouro` | Texto | Não | Logradouro do endereço | `"Rua Exemplo"` |
| `localidade` | Texto | Sim | Município do endereço | `"São Paulo"` |
| `uf` | Texto | Sim | Unidade Federativa do endereço | `"SP"` |

### Resposta

| Campo | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| `cep` | Texto | CEP do endereço sem formatação | `"12345678"` |
| `cep_formatado` | Texto | CEP do endereço com formatação | `"12345-678"` |
| `tipo` | Texto | Tipo de endereço | `"Logradouro"` |
| `caixa_postal` | Booleano | Indicador se é caixa postal | `false` |
| `nome` | Texto | Nome do endereço (se aplicável) | `null` |
| `nome_abreviado` | Texto | Nome abreviado do endereço (se aplicável) | `null` |
| `tipo_logradouro` | Texto | Tipo de logradouro (se aplicável) | `"Rua"` |
| `nome_logradouro` | Texto | Nome do logradouro (se aplicável) | `"Exemplo"` |
| `logradouro` | Texto | Logradouro do endereço (se aplicável) | `"Rua Exemplo"` |
| `complemento` | Texto | Complemento do endereço (se aplicável) | `null` |
| `bairro` | Texto | Bairro, distrito ou povoado do endereço (se aplicável) | `"Exemplo"` |
| `bairro_abreviado` | Texto | Bairro abreviado do endereço (se aplicável) | `"Exemplo"` |
| `localidade` | Texto | Município, distrito ou povoado do endereço | `"São Paulo"` |
| `uf` | Texto | Unidade Federativa do endereço | `"SP"` |

### Erros

| Código | Erro                     |
| ------ | ------------------------ |
| `400`  | `REQUISICAO_INVALIDA`    |
| `403`  | `PLANO_INATIVO`          |
| `403`  | `CREDITOS_INSUFICIENTES` |
| `404`  | `NAO_ENCONTRADO`         |
| `500`  | `ERRO`                   |
| `500`  | `ERRO_INTERNO`           |
| `503`  | `SERVICO_INDISPONIVEL`   |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v2/cep/buscar?logradouro=Rua%20Exemplo&localidade=S%C3%A3o%20Paulo&uf=SP' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

```json
[
  {
    "cep": "12345678",
    "cep_formatado": "12345-678",
    "tipo": "Logradouro",
    "caixa_postal": false,
    "nome": null,
    "nome_abreviado": null,
    "tipo_logradouro": "Rua",
    "nome_logradouro": "Exemplo",
    "logradouro": "Rua Exemplo",
    "complemento": null,
    "bairro": "Exemplo",
    "bairro_abreviado": "Exemplo",
    "localidade": "São Paulo",
    "uf": "SP"
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

## Timeout

A nossa API não retorna timeout. Caso seja necessário configurar um timeout na implantação, recomendamos utilizar **300 segundos**.

Verifique o timeout padrão da sua implantação, pois ele pode ser menor do que o tempo de resposta da API.

## Considerações

- As requisições "Consultar CEP" não consomem créditos (por tempo indeterminado)
- Cada requisição "Buscar CEP" consome R$ 0,05 dos créditos
- Somente as respostas com os códigos de status `200` e `404` consomem créditos
- Limite máximo de 1.000 resultados na requisição "Buscar CEP"
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte
