---
title: API CPF + Data de Nascimento
description: Web Service para consultar dados de pessoas físicas no Cadastro de Pessoas Físicas (CPF)
keywords: API, Webservice, Web Service, REST, JSON, CPF, Pessoa Física, Consulta, API, Brasil, Data de Nascimento, Validar Data de Nascimento, Validar Idade, Validar CPF, Consultar Data de Nascimento, Idade, Lei 15.211/2025, ECA Digital, Lei Felca
---

# API CPF + Data de Nascimento

[<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;">](https://god.gw.postman.com/run-collection/49657121-67b8bdd6-d2a3-4670-919d-23be3058fa49?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D49657121-67b8bdd6-d2a3-4670-919d-23be3058fa49%26entityType%3Dcollection%26workspaceId%3Daff38029-3b6a-4292-a751-b410e14cec19)

## Introdução

Esta API permite consultar informações sobre pessoas físicas registradas no Cadastro de Pessoas Físicas (CPF) do Brasil.

## Lei nº 15.211/2025 - ECA Digital

Utilize nossos dados como parte de um fluxo robusto de verificação de idade. Integre nossa solução a outras soluções de autenticação e biometria para atender aos requisitos da Lei nº 15.211/2025, conhecida como "ECA Digital", que exige a verificação de idade para acesso a conteúdos e serviços online destinados a menores de 18 anos.

## API Consultar CPF (Consultar pelo CPF + Data de Nascimento)

Consulta detalhes de um CPF específico.

### Endpoint

`GET https://consultar.io/api/v1/cpf/consultar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| `cpf` | Texto | Sim | Número do CPF (apenas números) | `12345678900` |
| `data_nascimento` | Texto | Sim | Data de nascimento (AAAA-MM-DD) | `1990-01-01` |

### Resposta

| Parâmetro | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| `cpf` | Texto | Número do CPF | `12345678900` |
| `nome` | Texto | Nome completo da pessoa | `MARIA DA SILVA` |
| `data_nascimento` | Texto | Data de nascimento | `1990-01-01` |
| `situacao` | Texto | Situação do CPF | `REGULAR` |
| `data_inscricao` | Texto | Data da inscrição no CPF | `2005-03-15` ou `anterior a 10/11/1990` |
| `digito_verificador` | Texto | Dígito verificador | `00` |
| `codigo_controle` | Texto | Código de controle da consulta | `2407.5A88.0E55.746B` |
| `data_emissao` | Texto | Data de emissão do comprovante | `2024-05-09` |
| `hora_emissao` | Texto | Hora de emissão do comprovante | `12:05:47` |
| `qrcode_url` | Texto | URL do QR Code para validação | `https://servicos.receita.fazenda.gov.br/Servicos/CPF/ca/ResultadoAut.asp?cp=87135740009&cc=24075A880E55746B&de=09052025&he=120547&dv=00&em=01` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/cpf/consultar?cpf=12345678900&data_nascimento=1990-01-01' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

```json
{
  "cpf": "12345678900",
  "nome": "MARIA DA SILVA SANTOS",
  "data_nascimento": "1990-01-01",
  "situacao": "REGULAR",
  "data_inscricao": "2005-03-15",
  "digito_verificador": "00",
  "codigo_controle": "2406.5A89.0E54.747B",
  "data_emissao": "2024-05-09",
  "hora_emissao": "12:05:47",
  "qrcode_url": "https://servicos.receita.fazenda.gov.br/Servicos/CPF/ca/ResultadoAut.asp?cp=12345678900&cc=24065A890E54747B&de=09052024&he=120547&dv=00&em=01"
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

- Cada requisição "Consultar CPF" consome R$ 0,20 dos créditos
- Somente as respostas com os códigos de status `200` e `404` consomem créditos
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte

## Termos de Uso

Consulte os Termos de Uso em: [https://consultar.io/termos/](https://consultar.io/termos/?utm_source=docs&utm_medium=referral&utm_campaign=teste-gratis)