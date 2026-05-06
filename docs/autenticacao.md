---
title: Autenticação
description: Como autenticar nas APIs e Web Services do Consultar.IO usando Token de API
keywords: Autenticação, Token, API, Webservice, Web Service, REST, Consultar.IO
---

# Autenticação

Todas as APIs requerem autenticação usando Autenticação por Token.

## Criar Token de API

Para obter um token de autenticação:

1. Acesse a página: [https://consultar.io/painel/token/](https://consultar.io/painel/token/?utm_source=docs&utm_medium=referral&utm_campaign=link)
2. Clique no botão `Criar Token`
3. Copie o token gerado e guarde-o em um local seguro, pois ele não será exibido novamente.

## Autenticação por Token

O token deve ser enviado no cabeçalho `Authorization` da requisição:

`Authorization: Token <seu-token>`

## Considerações

- O token de autenticação deve ser mantido em segurança
- Em caso de comprometimento do token, entre em contato com o Suporte

## Termos de Uso

Consulte os Termos de Uso em: [https://consultar.io/termos/](https://consultar.io/termos/?utm_source=docs&utm_medium=referral&utm_campaign=teste-gratis)