---
title: Configuração Sistemas Web com Tomcat
description: Configuração geral para subir aplicações TomCat
published: true
date: 2020-04-29T02:43:10.951Z
tags: 
---

# Configurações dos Sistemas Web - TomCat

Para subir localmente uma aplicação Web que utiliza o servidor Apache Tomcat, seguir os seguintes passos:

- Instalar na máquina o TomCat 8.5 (executar o instalador)
- Verificar na unidade C: se existe a pasta Na_Info, se já existir criar dentro dela a pasta "SrvWeb", se não existir criar conforme exemplo: C:/Na_Info/SrvWeb.

- Colocar a pasta do apache, que geralmente esta no caminho C:\Program Files\Apache Software Foundation, dentro dessa pasta (SrvWeb), renomear com a versão e a porta conforme exemplo: tomcat8.5.8080

- Parar a execução do Apache que esta sendo executado como um serviço.

- Dentro da pasta do tomcat, localizar a pasta "webapps" e dentro dela colocar o artefato ***.war*** da aplicação.

- Startar o serviço Apache.

## Conexão com Banco de Dados

Verificar se dentro da pasta tomcat8.5.8080 > conf > Catalina > localhost será criado o xml da aplicação com a configuração do banco de dados, caso não tenha sido criada, será necessário criá-la coforme exemplo:


