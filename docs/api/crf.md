---
title: API CRF
description: Web Service para consultar dados de profissionais no Conselho Regional de Farmácia (CRF)
keywords: API, Web Service, REST, JSON, CRF, Profissional, Estabelecimento, Consulta, API, Brasil
---

# API CRF

## Introdução

Esta API permite consultar profissionais e estabelecimentos registrados nos Conselhos Regionais de Farmácia (CRF) do Brasil.

## API Consultar CRF (Consultar pelo CRF)

Consulta detalhes de um registro específico.

### Endpoint

`GET /api/v1/crf/consultar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| `uf` | Texto | Sim | UF do CRF | `SP` |
| `numero_registro` | Texto | Sim | Número do registro (até 7 dígitos, zeros à esquerda são removidos) | `12344` |

### Resposta

| Parâmetro | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| `uf` | Texto | UF do CRF | `SP` |
| `numero_registro` | Texto | Número do registro | `1234567` |
| `categoria` | Texto | Categoria do profissional | `FARMACÊUTICO` |
| `nome_razao_social` | Texto | Nome ou razão social do profissional | `JOÃO DA SILVA` |
| `situacao` | Texto | Situação do registro | `DEFINITIVO` |
| `cidade` | Texto | Cidade do registro | `SÃO PAULO` |
| `data_inscricao` | Texto | Data de inscrição (YYYY-MM-DD) | `2025-08-29` |
| `data_inscricao_formatada` | Texto | Data de inscrição formatada (DD/MM/AAAA) | `29/08/2025` |
| `cpf` | Texto | CPF do profissional | `15685971001` |
| `cpf_formatado` | Texto | CPF do profissional formatado | `156.859.710-01` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/crf/consultar?uf=sp&numero_registro=12344' -H 'Authorization: Token <seu-token>'
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

- Cada requisição "Consultar CRF" consome R$ 0,20 dos créditos
- Somente as respostas com os códigos de status `200` e `404` consomem créditos
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte
