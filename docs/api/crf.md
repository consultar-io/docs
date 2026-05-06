---
title: API CRF
description: Web Service para consultar dados de profissionais no Conselho Regional de Farmácia (CRF)
keywords: API, Webservice, Web Service, REST, JSON, CRF, Profissional, Estabelecimento, Consulta, API, Brasil
---

# API CRF

[<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;">](https://god.gw.postman.com/run-collection/49657121-67b8bdd6-d2a3-4670-919d-23be3058fa49?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D49657121-67b8bdd6-d2a3-4670-919d-23be3058fa49%26entityType%3Dcollection%26workspaceId%3Daff38029-3b6a-4292-a751-b410e14cec19)

[![Run in Insomnia}](https://insomnia.rest/images/run.svg)](https://insomnia.rest/run/?label=APIs%20Consultar.IO&uri=https%3A%2F%2Fraw.githubusercontent.com%2Fconsultar-io%2Finsomnia%2Frefs%2Fheads%2Fmain%2Finsomnia.yaml)

[<img src="https://fetch.usebruno.com/button.svg" alt="Fetch in Bruno" style="width: 130px; height: 30px;" width="128" height="32">](https://fetch.usebruno.com?url=https%3A%2F%2Fgithub.com%2Fconsultar-io%2Fbruno.git)

## Introdução

Esta API permite consultar profissionais e estabelecimentos registrados nos Conselhos Regionais de Farmácia (CRF) do Brasil.

## API Consultar CRF (Consultar pelo CRF)

Consulta detalhes de um registro específico.

### Endpoint

`GET https://consultar.io/api/v1/crf/consultar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| `uf` | Texto | Sim | UF do registro | `SP` |
| `cidade` | Texto | Sim | Cidade do registro | `SÃO PAULO` |
| `numero_registro` | Texto | Sim | Número do registro (até 7 dígitos, zeros à esquerda são removidos) | `1234567` |

### Resposta

| Parâmetro | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| `uf` | Texto | UF do registro | `SP` |
| `numero_registro` | Texto | Número do registro | `1234567` |
| `categoria` | Texto | Categoria do profissional | `FARMACÊUTICO` |
| `nome_razao_social` | Texto | Nome do profissional | `JOÃO DA SILVA` |
| `situacao` | Texto | Situação do registro | `DEFINITIVO` |
| `cidade` | Texto | Cidade do registro | `SÃO PAULO` |
| `data_inscricao` | Texto | Data de inscrição (YYYY-MM-DD) | `2025-08-29` |
| `data_inscricao_formatada` | Texto | Data de inscrição formatada (DD/MM/AAAA) | `29/08/2025` |
| `cpf` | Texto | CPF do profissional (se informado) | `15685971001` |
| `cpf_formatado` | Texto | CPF do profissional formatado (se informado) | `156.859.710-01` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/crf/consultar?uf=SP&cidade=SÃO+PAULO&numero_registro=1234567' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

```json
{
  "uf": "SP",
  "numero_registro": "1234567",
  "categoria": "FARMACÊUTICO",
  "nome_razao_social": "JOÃO DA SILVA",
  "situacao": "DEFINITIVO",
  "cidade": "SÃO PAULO",
  "data_inscricao": "2025-08-29",
  "data_inscricao_formatada": "29/08/2025",
  "cpf": "15685971001",
  "cpf_formatado": "156.859.710-01"
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

## Timeout

A nossa API não retorna timeout. Caso seja necessário configurar um timeout na implantação, recomendamos utilizar **300 segundos**.

Verifique o timeout padrão da sua implantação, pois ele pode ser menor do que o tempo de resposta da API.

## Considerações

- Cada requisição "Consultar CRF" consome R$ 0,20 dos créditos
- Somente as respostas com os códigos de status `200` e `404` consomem créditos
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte

## Termos de Uso

Consulte os Termos de Uso em: [https://consultar.io/termos/](https://consultar.io/termos/?utm_source=docs&utm_medium=referral&utm_campaign=teste-gratis)