---
title: API Inscrição Estadual
description: Web Service para consultar dados de Inscrições Estaduais no SINTEGRA
keywords: API, Web Service, REST, JSON, Inscrição Estadual, IE, SINTEGRA, SEFAZ, Produtor Rural, Produtores Rurais, CNPJ, CPF
---

# API Inscrição Estadual (Versão 2)

## Introdução

Esta API permite consultar informações sobre Inscrições Estaduais no SINTEGRA. A consulta de Inscrições Estaduais é realizada pelo CNPJ ou CPF do contribuinte, juntamente com a UF.

Também é possível consultar informações de Produtores Rurais pelo CPF.

## API Consultar IE por UF (Consultar pelo CNPJ ou CPF)

Consulta detalhes de uma Inscrição Estadual específica.

### Endpoint

`GET /api/v2/ie/consultar`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| `uf` | Texto | Sim | Unidade Federativa da Inscrição Estadual | `SP` |
| `cnpj` ou `cpf` | Texto | Sim | CNPJ ou CPF do contribuinte | `61585865150633` |

### Resposta

| Campo | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| `cnpj` | Texto | CNPJ ou CPF do contribuinte | `"61585865150633"` |
| `razao_social` | Texto | Razão social da empresa | `"RAIA DROGASIL S/A"` |
| `nome_fantasia` | Texto | Nome fantasia da empresa | `""` |
| `uf_ie` | Texto | Unidade Federativa da Inscrição Estadual | `"SP"` |
| `ie` | Texto | Número da Inscrição Estadual | `"535612879117"` |
| `tipo_ie` | Texto | Tipo da Inscrição Estadual (se informado) | `"NÃO INFORMADO"` |
| `situacao_ie` | Texto | Situação atual da Inscrição Estadual | `"HABILITADO"` |
| `situacao_cnpj` | Texto | Status do CNPJ (se informado) | `"NÃO INFORMADO"` |
| `data_situacao_uf` | Data | Data da última atualização da situação (se informado) | `"22/06/2016"` |
| `data_inicio` | Data | Data de início da Inscrição Estadual (se informado) | `"22/06/2016"` |
| `data_fim` | Data | Data de encerramento da Inscrição Estadual (se informado) | `""` |
| `cnae_principal_codigo` | Texto | Código CNAE da atividade principal (se informado) | `"4771701"` |
| `regime_tributacao` | Texto | Regime de tributação (se informado) | `"NORMAL - REGIME PERIÓDICO DE APURAÇÃO"` |
| `ie_destinatario` | Texto | Indicador de obrigatoriedade de IE do destinatário (se informado) | `"NÃO INFORMADO"` |
| `porte_empresa` | Texto | Porte da empresa (se informado) | `"NÃO INFORMADO"` |
| `credito_presumido` | Texto | Indicador dos créditos presumido (se informado) | `"NÃO INFORMADO"` |
| `tipo_produtor` | Texto | Indicador se é produtor rural (se informado) | `"NÃO INFORMADO"` |
| `logradouro` | Texto | Nome do logradouro (se informado) | `"AVENIDA INDEPENDENCIA"` |
| `numero` | Texto | Número do endereço (se informado) | `"2906"` |
| `complemento` | Texto | Complemento do endereço (se informado) | `""` |
| `bairro` | Texto | Bairro (se informado) | `"ALEMAES"` |
| `cep` | Texto | CEP (se informado) | `"13416-240"` |
| `uf` | Texto | UF do endereço do estabelecimento | `"SP"` |
| `municipio_codigo` | Texto | Código IBGE do município (se informado) | `"3538709"` |
| `municipio_descricao` | Texto | Nome do município (se informado) | `"PIRACICABA"` |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v2/ie/consultar?uf=SP&cnpj=61585865150633' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200) - CNPJ

```json
[
  {
    "cnpj": "61585865150633",
    "razao_social": "RAIA DROGASIL S/A",
    "nome_fantasia": "",
    "uf_ie": "SP",
    "ie": "535612879117",
    "tipo_ie": "NÃO INFORMADO",
    "situacao_ie": "HABILITADO",
    "situacao_cnpj": "NÃO INFORMADO",
    "data_situacao_uf": "22/06/2016",
    "data_inicio": "22/06/2016",
    "data_fim": "",
    "cnae_principal_codigo": "4771701",
    "regime_tributacao": "NORMAL - REGIME PERIÓDICO DE APURAÇÃO",
    "ie_destinatario": "NÃO INFORMADO",
    "porte_empresa": "NÃO INFORMADO",
    "credito_presumido": "NÃO INFORMADO",
    "tipo_produtor": "NÃO INFORMADO",
    "logradouro": "AVENIDA INDEPENDENCIA",
    "numero": "2906",
    "complemento": "",
    "bairro": "ALEMAES",
    "cep": "13416240",
    "uf": "SP",
    "municipio_codigo": "3538709",
    "municipio_descricao": "PIRACICABA"
  }
]
```

#### Exemplo de Resposta de Sucesso (200) - CPF

```json
[
  {
    "cnpj": "35488964053",
    "razao_social": "MIGUEL RICARDO CAVALCANTI",
    "nome_fantasia": "FAZENDA DA CUNHA",
    "uf_ie": "MT",
    "ie": "698741950",
    "tipo_ie": "IE DE PRODUTOR RURAL",
    "situacao_ie": "HABILITADO",
    "situacao_cnpj": "SEM RESTRIÇÃO",
    "data_situacao_uf": "07/03/2005",
    "data_inicio": "07/03/2005",
    "data_fim": "",
    "cnae_principal_codigo": "115600",
    "regime_tributacao": "NORMAL",
    "ie_destinatario": "OBRIGATÓRIA",
    "porte_empresa": "",
    "credito_presumido": "",
    "tipo_produtor": "NÃO",
    "logradouro": "RODOVIA MT 123 KM 456",
    "numero": "SN",
    "complemento": "",
    "bairro": "ZONA RURAL",
    "cep": "78467899",
    "uf": "MT",
    "municipio_codigo": "5105259",
    "municipio_descricao": "LUCAS DO RIO VERDE"
  },
  {
    "cnpj": "35488964053",
    "razao_social": "MIGUEL RICARDO CAVALCANTI",
    "nome_fantasia": "FAZENDA CARVALHO",
    "uf_ie": "MT",
    "ie": "292692800",
    "tipo_ie": "IE DE PRODUTOR RURAL",
    "situacao_ie": "HABILITADO",
    "situacao_cnpj": "SEM RESTRIÇÃO",
    "data_situacao_uf": "02/06/2011",
    "data_inicio": "02/06/2011",
    "data_fim": "",
    "cnae_principal_codigo": "154700",
    "regime_tributacao": "",
    "ie_destinatario": "OBRIGATÓRIA",
    "porte_empresa": "",
    "credito_presumido": "",
    "tipo_produtor": "NÃO",
    "logradouro": "RODOVIA MT 345 KM 678",
    "numero": "SN",
    "complemento": "",
    "bairro": "ZONA RURAL",
    "cep": "78467899",
    "uf": "MT",
    "municipio_codigo": "5105259",
    "municipio_descricao": "LUCAS DO RIO VERDE"
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

## API Consultar IE em Todas as UFs (Consultar pelo CNPJ ou CPF)

Consulta detalhes de todas as Inscrições Estaduais em todas as UFs.

### Endpoint

`GET /api/v2/ie/consultar/todas`

### Requisição

| Parâmetro | Tipo | Obrigatório | Descrição | Exemplo |
| --- | --- | --- | --- | --- |
| `cnpj` ou `cpf` | Texto | Sim | CNPJ ou CPF do contribuinte | `61585865150633` |

### Resposta

| Campo | Tipo | Descrição | Exemplo |
| --- | --- | --- | --- |
| `uf` | Texto | Unidade Federativa | `"SP"` |
| `status_code` | Número | Código de status (`200`, `404`, `503` ou `500`) | `200` |
| `success` | Booleano | Sucesso da consulta (`true` ou `false`) | `true` |
| `message` | Texto | Mensagem de erro | `""` |
| `results` | Array | Resultados da consulta | `[ ... ]` |
| `results.cnpj` | Texto | CNPJ ou CPF do contribuinte | `"61585865150633"` |
| `results.razao_social` | Texto | Razão social da empresa | `"RAIA DROGASIL S/A"` |
| `results.nome_fantasia` | Texto | Nome fantasia da empresa | `""` |
| `results.uf_ie` | Texto | Unidade Federativa da Inscrição Estadual | `"SP"` |
| `results.ie` | Texto | Número da Inscrição Estadual | `"535612879117"` |
| `results.tipo_ie` | Texto | Tipo da Inscrição Estadual (se informado) | `"NÃO INFORMADO"` |
| `results.situacao_ie` | Texto | Situação atual da Inscrição Estadual | `"HABILITADO"` |
| `results.situacao_cnpj` | Texto | Status do CNPJ (se informado) | `"NÃO INFORMADO"` |
| `results.data_situacao_uf` | Data | Data da última atualização da situação (se informado) | `"22/06/2016"` |
| `results.data_inicio` | Data | Data de início da Inscrição Estadual (se informado) | `"22/06/2016"` |
| `results.data_fim` | Data | Data de encerramento da Inscrição Estadual (se informado) | `""` |
| `results.cnae_principal_codigo` | Texto | Código CNAE da atividade principal (se informado) | `"4771701"` |
| `results.regime_tributacao` | Texto | Regime de tributação (se informado) | `"NORMAL - REGIME PERIÓDICO DE APURAÇÃO"` |
| `results.ie_destinatario` | Texto | Indicador de obrigatoriedade de IE do destinatário (se informado) | `"OBRIGATÓRIA"` |
| `results.porte_empresa` | Texto | Porte da empresa (se informado) | `"NÃO INFORMADO"` |
| `results.credito_presumido` | Texto | Indicador dos créditos presumido (se informado) | `"NÃO INFORMADO"` |
| `results.tipo_produtor` | Texto | Indicador se é produtor rural (se informado) | `"NÃO INFORMADO"` |
| `results.logradouro` | Texto | Nome do logradouro (se informado) | `"AVENIDA INDEPENDENCIA"` |
| `results.numero` | Texto | Número do endereço (se informado) | `"2906"` |
| `results.complemento` | Texto | Complemento do endereço (se informado) | `""` |
| `results.bairro` | Texto | Bairro (se informado) | `"ALEMAES"` |
| `results.cep` | Texto | CEP (se informado) | `"13416-240"` |
| `results.uf` | Texto | UF do endereço do estabelecimento | `"SP"` |
| `results.municipio_codigo` | Texto | Código IBGE do município (se informado) | `"3538709"` |
| `results.municipio_descricao` | Texto | Nome do município (se informado) | `"PIRACICABA"` |

### Códigos de Status por UF (status_code)

| Código de Status | Descrição                                |
| ---------------- | ---------------------------------------- |
| `200`            | Contribuinte encontrado na SEFAZ.        |
| `404`            | Contribuinte não encontrado na SEFAZ.    |
| `503`            | SEFAZ está temporariamente indisponível. |
| `500`            | Aconteceu um erro na consulta.           |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v2/ie/consultar/todas?cnpj=61585865150633' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

```json
[
  {
    "uf": "AC",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "AL",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "AM",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "AP",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "BA",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "CE",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "DF",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "ES",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "GO",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "MA",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "MG",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "MS",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "MT",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "PA",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "PB",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "PE",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "PI",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "PR",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "RJ",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "RN",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "RO",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "RR",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "RS",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "SC",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "SE",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  },
  {
    "uf": "SP",
    "status_code": 200,
    "success": true,
    "message": "",
    "results": [
      {
        "cnpj": "61585865150633",
        "razao_social": "RAIA DROGASIL S/A",
        "nome_fantasia": "",
        "uf_ie": "SP",
        "ie": "535612879117",
        "tipo_ie": "NÃO INFORMADO",
        "situacao_ie": "HABILITADO",
        "situacao_cnpj": "NÃO INFORMADO",
        "data_situacao_uf": "22/06/2016",
        "data_inicio": "22/06/2016",
        "data_fim": "",
        "cnae_principal_codigo": "4771701",
        "regime_tributacao": "NORMAL - REGIME PERIÓDICO DE APURAÇÃO",
        "ie_destinatario": "NÃO INFORMADO",
        "porte_empresa": "NÃO INFORMADO",
        "credito_presumido": "NÃO INFORMADO",
        "tipo_produtor": "NÃO INFORMADO",
        "logradouro": "AVENIDA INDEPENDENCIA",
        "numero": "2906",
        "complemento": "",
        "bairro": "ALEMAES",
        "cep": "13416240",
        "uf": "SP",
        "municipio_codigo": "3538709",
        "municipio_descricao": "PIRACICABA"
      }
    ]
  },
  {
    "uf": "TO",
    "status_code": 404,
    "success": false,
    "message": "Contribuinte não encontrado no banco de dados da SEFAZ da UF informada.",
    "results": []
  }
]
```

#### Exemplo de Resposta de Erro (500)

```json
{
  "error": "ERRO_INTERNO",
  "message": "Ocorreu um erro no nosso sistema. Por favor, tente novamente mais tarde."
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

- Cada requisição "Consultar Inscrição Estadual" consome R$ 0,20 dos créditos
- Cada requisição "Consultar Todas das IEs" consome R$ 5,40 dos créditos (R$ 0,20 por UF)
- Somente as respostas com os códigos de status `200` e `404` consomem créditos
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte
