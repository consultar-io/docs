---
title: API CEP (Versão 1) - Versão em Depreciação
description: Versão 1 - Versão em Depreciação
keywords: API CEP, Versão 1, Versão em Depreciação, Consultar.IO, Consultar IO
---

# API CEP (Versão 1)

!!! warning "Versão em Depreciação"

    Essa versão da API de CEP está em depreciação e será descontinuada em 28/02/2026. Migre para a [Versão 2](../../api/cep.md).

## Introdução

Esta API permite consultar os dados de um endereço a partir de um CEP.

## API Consultar CEP (Consultar pelo CEP)

Consulta detalhes de um CEP específico.

### Endpoint

`GET https://consultar.io/api/v1/cep/consultar`

### Requisição

| Parâmetro | Tipo  | Obrigatório | Descrição                   | Exemplo    |
| --------- | ----- | ----------- | --------------------------- | ---------- |
| `cep`     | Texto | Sim         | CEP do endereço (8 dígitos) | `12345678` |

### Resposta

| Campo        | Tipo   | Descrição                      | Exemplo         |
| ------------ | ------ | ------------------------------ | --------------- |
| `cep`        | Texto  | CEP do endereço sem formatação | `"12345678"`    |
| `uf`         | Texto  | Unidade Federativa do endereço | `"SP"`          |
| `localidade` | Texto  | Município do endereço          | `"São Paulo"`   |
| `bairro`     | Texto  | Bairro do endereço             | `"Exemplo"`     |
| `logradouro` | Texto  | Logradouro do endereço         | `"Rua Exemplo"` |
| `latitude`   | Número | Não disponível                 | `null`          |
| `longitude`  | Número | Não disponível                 | `null`          |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/cep/consultar?cep=12345678' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

```json
{
  "cep": "12345678",
  "uf": "SP",
  "localidade": "São Paulo",
  "bairro": "Exemplo",
  "logradouro": "Rua Exemplo",
  "latitude": null,
  "longitude": null
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

| Código | Erro (error) | Descrição |
| --- | --- | --- |
| `400` | `REQUISICAO_INVALIDA` | Veja a mensagem de erro (message) para mais detalhes. |
| `403` | `PLANO_INATIVO` | Plano inativo. Faça uma Recarga. |
| `403` | `CREDITOS_INSUFICIENTES` | Créditos insuficientes. Faça uma Recarga. |
| `404` | `NAO_ENCONTRADO` | Registro não encontrado. |
| `500` | `ERRO` | Veja a mensagem de erro (message) para mais detalhes. |
| `500` | `ERRO_INTERNO` | Ocorreu um erro inesperado no nosso sistema. |
| `503` | `SERVICO_INDISPONIVEL` | Veja a mensagem de erro (message) para mais detalhes. |

## Observações

- O CEP pode ser informado com ou sem hífen

## Limites e Considerações

- As requisições "Consultar CEP" não consomem créditos (por tempo indeterminado)
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte
