---
title: Configurar o Wildfly 15 no Client
description: Configurar um servidor Wildfly 15 e alterar as portas de acesso
published: true
date: 2020-07-23T17:29:07.810Z
tags: 
---

# Configurar o Wildfly 15 no cliente
Passo a passo para configurar o wildfly 15 em um servidor do cliente

# Passo 1

* Copie a pasta do Wildfly15 e renomeie a pasta com o valor da porta. Ex: wildfly15_8084

* Configurar a porta no arquivo standalone.xml -> wildfly15_8084\standalone\configuration

````
<socket-binding-group name="standard-sockets" default-interface="public" port-offset="${jboss.socket.binding.port-offset:100}">
````
* O valor que definir no port-offset , você soma ao valor da porta padrão que é 8080 , exemplo : Se eu defini o valor em 100 no port-offset a minha porta vai ser 8180 -> 8080 + 100

* Após definir o valor da porta , alterar o arquivo service.bat ->wildfly15_8180\bin\service. Definir o nome do serviço


````
rem defaults
set SHORTNAME=nea_wildfly_8180
rem NO quotes around the display name here !
set DISPLAYNAME=nea_wildfly_8180
rem NO quotes around the description here !
set DESCRIPTION=nea_wildfly_8180

````

* E depois só instalar o serviço Wildfly no prompt de comando

````
D:\Na_Info\SRVWEB\wildfly15_8180\bin\service> service install
````
* Pronto serviço instalado com a porta definida


