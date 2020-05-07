---
title: Configuração da IDE Intellij
description: Configurações para utilizar a IDE Intellij 
published: true
date: 2020-05-07T15:28:33.140Z
tags: ide, intellij
---

# IDE Intellij com TomCat8.0

* Para utilizar a IDE Intellij nos projetos Java será necessário configurar de acordo com o servidor que será utilizado, Wildfly13.0/15.0 ou Tomcat8.0.

## Download da IDE

* Acessar o site da JetBrains https://www.jetbrains.com/. Procurar pela IDE Intellij, e clicar em Download. Será apresentado duas opções:


![instalacao.png](/imagens/instalacao.png){.align-center}

> instalar a versão **Ultimate**.

## Abrindo o projeto na IDE

* Após a instalação, abrir o projeto que deseja trabalhar:

![open.png](/imagens/open.png){.align-center}

> Procurar o caminho onde está o projeto e abrir. Após abrir a IDE apresentará mensagens no canto inferior direito, sobre configurações e dependências (Maven) que deverão ser importadas no projeto.



## Configurando TomCat 8.0 no projeto

* Ao abrir o projeto, localizar no canto superior o botão de "Add Configuration".

![add.png](/imagens/add.png){.align-center}

> Certificar de ter instalado o TomCat8.0 em sua máquina, para isso verificar em C:\Program Files\Apache Software Foundation

* Após clicar nesse botão, será aberta a tela para configurarmos o servidor. Clicar no sinal de "+" que aparecerá no canto superior esquerdo.

![add3.png](/imagens/add3.png){.align-center}

* Será aberta uma lista com com vários tipos de configurações de servidores. Procurar a "Tomcat Server", após clicar em "Local".

![tomcat2.png](/imagens/tomcat2.png){.align-center}

* Na tela que será aberta localizar "Application Server" e clicar em "Configure"

![configure.png](/imagens/configure.png){.align-center}

* Inserir no campo "Tomcat Home" e "Tomcat base directory" o caminho onde esta o Tomcar8.0

![apache.png](/imagens/apache.png){.align-center}

* Depois, clicar em OK. Será retornado para a tela de configuração do servidor. Observar no canto inferior direito que aparecerá uma lâmpada vermelha escrito "Fix". Isso ocorre porque é necessário fixar dentro do servidor o artefato que será feito o deploy. Clicar nessa lâmpada para fixar o artefato

![fix.png](/imagens/fix.png){.align-center}

* Escolher o artefafo que será feito o deploy. Geralmente será o com extensão "exploded"

![artefato.png](/imagens/artefato.png){.align-center}

> Após escolher o artefato observar o contexto da aplicação logo abaixo, pois será necessário mapear a URL correta do projeto.

* Deopis de verificar se todas as configurações estçao corretas clicar em OK.A IDE estará pronta para ser utilizada com o Tomcat8.0

* Confira as configurações:

![url.png](/imagens/url.png){.align-center}

![java2.png](/imagens/java2.png){.align-center}
 
![porta.png](/imagens/porta.png){.align-center}

# IDE Intellij com WildFly13/15