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

`GET https://consultar.io/api/v1/ie/consultar`

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

## Limites e Considerações

- Cada requisição "Consultar Inscrição Estadual" consome R$ 0,20 dos créditos
- Somente as respostas com os códigos de status `200` e `404` consomem créditos
- Todas as requisições são registradas no histórico de transações
- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte
