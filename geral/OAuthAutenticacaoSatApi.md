---
title: Autenticação Spring Security - OAuth2
description: Autenticação SAT API
published: true
date: 2020-08-11T13:01:47.183Z
tags: sat, autenticação, api
---

# Autenticar com OAuth2

- Utilizando o INSOMINIA/POSTMAN com metodo POST com a rota http://localhost:81/sat-api/oauth/token

- Alterar o tipo de "Structured" para "Form URL Enconded"

- No campos preecher como a seguir:
	<br/>
	grant_type : password
	username : suporte
	password : senhaDia (Se suporte)
  <br/>
	
- Na aba Auth alterar para "Basic Auth" e preecher com o usarname e password que constam na classe EnumAplicativoCliente.java, onde o "client" sera o usarname e a "secret" sera a password.

- Será retornado o token de acesso. Nas requisiçoes que serão realizadas, alterar o Auth para Bearer, no campo token colar o token que foi retornado anteriormente e no prefix escrever Bearer. Realizar isso para todas a requisições/rotas.

