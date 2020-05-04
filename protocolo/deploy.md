---
title: Deploy Sistema Protocolo
description: 
published: true
date: 2020-05-04T03:44:28.065Z
tags: protocolo, deploy
---

# Deploy do Sistema Protocolo

1. Gerar arquivo **.war** do projeto
2. Substituir esse arquivo para a pasta \\192.168.10.233\opt\aplicativo
3. Abrir o aplicativo MobaXterm e logar no SRV com as credenciais abaixo:
**host:** 192.168.10.233
**user:** root
**pass:** n519631a*
4. Navegar através do terminal até a pasta \opt\aplicativo
5. Executar o script de deploy com o comando abaixo:
 ```
 ./_deploy_protocolo.sh
 ```
* Obs.: caso de falha no deploy executar comando - killall java - para matar processos e
executar o sc
6. Acessar o endereço http://192.168.10.233/ e verificar se o deploy teve sucesso