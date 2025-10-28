---
title: API Inscrição Estadual (Versão 1) - Versão em Depreciação
description: Versão 1 - Versão em Depreciação
keywords: API Inscrição Estadual, Versão 1, Versão em Depreciação, Consultar.IO, Consultar IO
---

# API Inscrição Estadual (Versão 1)

!!! warning "Versão em Depreciação"

    Essa versão da API de Inscrição Estadual está em depreciação e será descontinuada em 28/02/2026. Migre para a [Versão 2](../../api/inscricao-estadual.md).

## Introdução

Esta API permite consultar informações sobre Inscrições Estaduais no SINTEGRA/CCC/SEFAZ. A consulta pode ser realizada utilizando o CNPJ ou CPF do contribuinte, juntamente com a UF.

## API Consultar Inscrição Estadual (Consultar pelo CNPJ ou CPF)

Consulta detalhes de uma Inscrição Estadual específica.

### Endpoint

`GET /api/v1/ie/consultar`

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
| `tipo_ie` | Texto | Tipo da Inscrição Estadual | `"IE NORMAL"` |
| `situacao_ie` | Texto | Situação atual da Inscrição Estadual | `"HABILITADO"` |
| `situacao_cnpj` | Texto | Status do CNPJ | `"SEM RESTRIÇÃO"` |
| `data_situacao_uf` | Data | Data da última atualização da situação | `"22/06/2016"` |
| `data_inicio` | Data | Data de início da Inscrição Estadual | `"22/06/2016"` |
| `data_fim` | Data | Data de encerramento da Inscrição Estadual (se houver) | `""` |
| `cnae_principal_codigo` | Texto | Código CNAE da atividade principal | `"4771701"` |
| `regime_tributacao` | Texto | Regime de tributação | `"NORMAL"` |
| `ie_destinatario` | Texto | Indicador de obrigatoriedade de IE do destinatário | `"OBRIGATÓRIA"` |
| `porte_empresa` | Texto | Porte da empresa | `""` |
| `credito_presumido` | Texto | Indicador dos créditos presumido | `""` |
| `tipo_produtor` | Texto | Indicador se é produtor rural | `"NÃO"` |
| `logradouro` | Texto | Nome do logradouro | `"AVENIDA INDEPENDENCIA"` |
| `numero` | Texto | Número do endereço | `"2906"` |
| `complemento` | Texto | Complemento do endereço | `""` |
| `bairro` | Texto | Bairro | `"ALEMAES"` |
| `cep` | Texto | CEP | `"13416-240"` |
| `uf` | Texto | UF do endereço do estabelecimento | `"SP"` |
| `municipio_codigo` | Texto | Código IBGE do município | `"3538709"` |
| `municipio_descricao` | Texto | Nome do município | `"PIRACICABA"` |

### Erros

| Código HTTP | Erro                     |
| ----------- | ------------------------ |
| `400`       | `REQUISICAO_INVALIDA`    |
| `403`       | `PLANO_INATIVO`          |
| `403`       | `CREDITOS_INSUFICIENTES` |
| `404`       | `NAO_ENCONTRADO`         |
| `500`       | `ERRO`                   |
| `500`       | `ERRO_INTERNO`           |
| `503`       | `SERVICO_INDISPONIVEL`   |

### Exemplos

#### Exemplo de Requisição (cURL)

```bash
curl -X GET 'https://consultar.io/api/v1/ie/consultar?uf=SP&cnpj=61585865150633' -H 'Authorization: Token <seu-token>'
```

#### Exemplo de Resposta de Sucesso (200)

```json
{
  "cnpj": "61585865150633",
  "razao_social": "RAIA DROGASIL S/A",
  "nome_fantasia": "",
  "uf_ie": "SP",
  "ie": "535612879117",
  "tipo_ie": "IE NORMAL",
  "situacao_ie": "HABILITADO",
  "situacao_cnpj": "SEM RESTRIÇÃO",
  "data_situacao_uf": "22/06/2016",
  "data_inicio": "22/06/2016",
  "data_fim": "",
  "cnae_principal_codigo": "4771701",
  "regime_tributacao": "NORMAL",
  "ie_destinatario": "OBRIGATÓRIA",
  "porte_empresa": "",
  "credito_presumido": "",
  "tipo_produtor": "NÃO",
  "logradouro": "AVENIDA INDEPENDENCIA",
  "numero": "2906",
  "complemento": "",
  "bairro": "ALEMAES",
  "cep": "13416-240",
  "uf": "SP",
  "municipio_codigo": "3538709",
  "municipio_descricao": "PIRACICABA"
}
```

#### Exemplo de Resposta de Erro (404)

```json
{
  "error": "NAO_ENCONTRADO",
  "message": "Nenhum registro foi encontrado para os parâmetros informados."
}
```

## Limites e Considerações

- Cada requisição "Consultar Inscrição Estadual" consome R$ 0,20 dos créditos
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte
