---
title: API Geocodificação
description: Web Service para consultar a latitude e longitude de um endereço
keywords: API, Web Service, REST, JSON, Latitude, Longitude, Coordenadas, Geocodificação, Geocode, Geocoding, Endereço, Consulta, API, Brasil
---

# API Geocodificação (Versão 2)

[<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;">](https://god.gw.postman.com/run-collection/49657121-67b8bdd6-d2a3-4670-919d-23be3058fa49?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D49657121-67b8bdd6-d2a3-4670-919d-23be3058fa49%26entityType%3Dcollection%26workspaceId%3Daff38029-3b6a-4292-a751-b410e14cec19)

## Introdução

Esta API permite consultar a latitude e longitude de um endereço, também conhecido como geocodificação, em inglês, "geocode" ou "geocoding".

## API Consultar Geocodificação (Consultar pelo Endereço)

Consulta as coordenadas geográficas de um endereço específico.

### Endpoint

`GET https://consultar.io/api/v2/geocodificacao/consultar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| `endereco` | Texto | Sim | Endereço para consulta | `RUA EXEMPLO, 123, SAO PAULO, SP` |

### Resposta

| Campo | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| `licenca` | Texto | Licença de uso | `https://consultar.io/licencas` |
| `logradouro` | Texto | Logradouro do endereço | `Rua Exemplo` |
| `bairro` | Texto | Bairro do endereço | `Exemplo` |
| `localidade` | Texto | Município do endereço | `São Paulo` |
| `uf` | Texto | Unidade Federativa do endereço | `SP` |
| `latitude` | Número | Latitude do endereço | `-23.1234567` |
| `longitude` | Número | Longitude do endereço | `-46.1234567` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v2/geocodificacao/consultar?endereco=RUA+EXEMPLO,+123,SAO+PAULO,+SP' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

```json
{
  "licencas": "https://consultar.io/licencas",
  "logradouro": "Rua Exemplo",
  "bairro": "Exemplo",
  "localidade": "São Paulo",
  "uf": "SP",
  "latitude": -23.1234567,
  "longitude": -46.1234567
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

- Recomendamos informar pelo menos Logradouro, Número (se houver), Município e UF.
- Não recomendamos informar Complemento, Bairro e CEP.
- Não recomendamos usar abreviações.

## API Consultar Geocodificação Reversa (Consultar pela Latitude/Longitude)

Consulta o endereço a partir de coordenadas geográficas.

### Endpoint

`GET https://consultar.io/api/v2/geocodificacao/reversa/consultar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| `coordenadas` | Texto | Sim | Coordenadas geográficas (latitude e longitude) | `-23.1234567,-46.1234567` |

### Resposta

| Campo | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| `licencas` | Texto | Creditois da licença de uso do software e dados | `https://consultar.io/licencas` |
| `logradouro` | Texto | Logradouro mais próximo das coordenadas informadas | `Rua Exemplo` |
| `bairro` | Texto | Bairro do logradouro | `Exemplo` |
| `localidade` | Texto | Município do logradouro | `São Paulo` |
| `uf` | Texto | Unidade Federativa do logradouro | `SP` |
| `latitude` | Número | Latitude do logradouro | `-23.1234567` |
| `longitude` | Número | Longitude do logradouro | `-46.1234567` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v2/geocodificacao/reversa/consultar?coordenadas=-23.1234567,-46.1234567' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

```json
{
  "licencas": "https://consultar.io/licencas",
  "logradouro": "Rua Exemplo",
  "bairro": "Exemplo",
  "localidade": "São Paulo",
  "uf": "SP",
  "latitude": -23.1234567,
  "longitude": -46.1234567
}
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

- Cada requisição "Consultar Geocodificação" consome R$ 0,05 dos créditos
- Cada requisição "Consultar Geocodificação Reversa" consome R$ 0,05 dos créditos
- Somente as respostas com os códigos de status `200` e `404` consomem créditos
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte
