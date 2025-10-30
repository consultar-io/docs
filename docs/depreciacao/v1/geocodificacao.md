---
title: API Geocodificação (Versão 1) - Versão em Depreciação
description: Versão 1 - Versão em Depreciação
keywords: API Geocodificação, Versão 1, Versão em Depreciação, Consultar.IO, Consultar IO
---

# API Geocodificação (Versão 1)

!!! warning "Versão em Depreciação"

    Essa versão da API de Geocodificação está em depreciação e será descontinuada em 28/02/2026. Migre para a [Versão 2](../../api/geocodificacao.md).

## Introdução

Esta API permite consultar a latitude e longitude de um endereço, também conhecido como geocodificação, em inglês, "geocode" ou "geocoding".

## API Consultar Geocodificação (Consultar pelo Endereço)

Consulta as coordenadas geográficas de um endereço específico.

### Endpoint

`GET https://consultar.io/api/v1/geocodificacao/consultar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| `endereco` | Texto | Sim | Endereço para consulta | `RUA EXEMPLO, 123, SAO PAULO, SP` |

### Resposta

| Campo | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| `endereco_formatado` | Texto | Endereço formatado e normalizado | `"Rua Exemplo, São Paulo, SP"` |
| `latitude` | Número | Latitude do endereço | `-23.1234567` |
| `longitude` | Número | Longitude do endereço | `-46.1234567` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/geocodificacao/consultar?endereco=RUA+EXEMPLO,+123,SAO+PAULO,+SP' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

```json
{
  "endereco_formatado": "Rua Exemplo, São Paulo, SP",
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

## Códigos de Status HTTP

| Código | Erro | Descrição |
| --- | --- | --- |
| `400` | `REQUISICAO_INVALIDA` | Requisição inválida. Veja a mensagem para mais detalhes. |
| `403` | `PLANO_INATIVO` | Plano inativo. |
| `403` | `CREDITOS_INSUFICIENTES` | Créditos insuficientes. |
| `404` | `NAO_ENCONTRADO` | Registro não encontrado. |
| `500` | `ERRO` | Aconteceu um erro durante a consulta. Veja a mensagem para mais detalhes. |
| `500` | `ERRO_INTERNO` | Ocorreu um erro inesperado no nosso sistema. |
| `503` | `SERVICO_INDISPONIVEL` | Serviço está temporariamente indisponível. Veja a mensagem para mais detalhes. |

## Observações

- Recomendamos informar pelo menos Logradouro, Número (se houver), Município e UF.
- Não recomendamos informar Complemento, Bairro e CEP.
- Não recomendamos usar abreviações.

## Limites e Considerações

- Cada requisição "Consultar Geocodificação" consome R$ 0,05 dos créditos
- Somente as respostas com os códigos de status `200` e `404` consomem créditos
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte
