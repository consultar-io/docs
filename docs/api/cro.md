---
title: API CRO
description: Web Service para consultar dados de profissionais e estabelecimentos no Conselho Regional de Odontologia (CRO)
keywords: API, Web Service, REST, JSON, CRO, Profissional, Estabelecimento, Consulta, API, Brasil
---

# API CRO

[<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;">](https://god.gw.postman.com/run-collection/49657121-67b8bdd6-d2a3-4670-919d-23be3058fa49?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D49657121-67b8bdd6-d2a3-4670-919d-23be3058fa49%26entityType%3Dcollection%26workspaceId%3Daff38029-3b6a-4292-a751-b410e14cec19)

## Introdução

Esta API permite consultar e buscar informações sobre profissionais e estabelecimentos registrados nos Conselhos Regionais de Odontologia (CRO) do Brasil.

## API Consultar CRO (Consultar pelo CRO)

Consulta detalhes de um registro específico.

### Endpoint

`GET /api/v1/cro/consultar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| `uf` | Texto | Sim | UF do CRO | `SP` |
| `numero_registro` | Texto | Sim | Número do registro (até 7 dígitos, zeros à esquerda são removidos) | `123456` |
| `categoria` | Texto | Sim | Categoria do profissional/estabelecimento | `cd` |

### Resposta

| Parâmetro | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| `uf` | Texto | UF do CRO | `SP` |
| `numero_registro` | Texto | Número do registro | `123456` |
| `categoria` | Texto | Categoria do profissional/estabelecimento | `CIRURGIÃO-DENTISTA` |
| `nome_razao_social` | Texto | Nome ou razão social do profissional/estabelecimento | `JOÃO SILVA` |
| `situacao` | Texto | Situação do registro | `ATIVO` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/cro/consultar?uf=sp&numero_registro=123456&categoria=cd' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

```json
{
  "uf": "SP",
  "numero_registro": "123456",
  "categoria": "CIRURGIÃO-DENTISTA",
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

## API Buscar CRO (Buscar pelo Nome)

Realiza busca de profissionais/estabelecimentos pelo nome.

### Endpoint

`GET /api/v1/cro/buscar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| nome_razao_social | Texto | Sim | Nome ou razão social do profissional/estabelecimento | `joao silva` |
| categoria | Texto | Sim | Categoria do profissional/estabelecimento | `cd` |

### Resposta

| Parâmetro | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| uf | Texto | UF do CRO | `SP` |
| numero_registro | Texto | Número do registro | `123456` |
| categoria | Texto | Categoria do profissional/estabelecimento | `CIRURGIÃO-DENTISTA` |
| nome_razao_social | Texto | Nome ou razão social do profissional/estabelecimento | `JOÃO SILVA` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/cro/buscar?nome_razao_social=joao%20silva&categoria=cd' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200 OK)

```json
[
  {
    "uf": "SP",
    "numero_registro": "123456",
    "categoria": "CIRURGIÃO-DENTISTA",
    "nome_razao_social": "JOÃO SILVA"
  },
  {
    "uf": "SP",
    "numero_registro": "123457",
    "categoria": "CIRURGIÃO-DENTISTA",
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

## Categorias

| Código | Descrição |
| --- | --- |
| `cd` | Cirurgião Dentista |
| `tsb` | Técnico em Saúde Bucal |
| `tpd` | Técnico em Prótese Dentária |
| `asb` | Auxiliar em Saúde Bucal |
| `apd` | Auxiliar de Prótese Dentária |
| `estagiario` | Estagiário |
| `clinica-assistencia` | Clínica/Entidade Prestadora de Assistência Odontológica |
| `laboratorio` | Laboratório de Prótese Dentária |
| `comercio-industria` | Comércio/Indústria de Produtos Odontológicos |

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

- Cada requisição "Consultar CRO" consome R$ 0,20 dos créditos
- Cada requisição "Buscar CRO" consome R$ 0,20 dos créditos
- Somente as respostas com os códigos de status `200` e `404` consomem créditos
- Limite máximo de 100 resultados na "Buscar CRO"
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte
