---
title: Deploy Sistema Protocolo e Nota Fiscal
description: 
published: true
date: 2020-05-13T00:16:18.035Z
tags: protocolo, deploy, nfse
---

# Deploy dos Sistemas Protocolo e Nota Fiscal 

1. Gerar arquivo **.war** do projeto
2. Abrir o aplicativo MobaXterm e logar no SRV com as credenciais abaixo:

**host:** 192.168.10.233
**user:** ****
**pass:** ****


3. Substituir(Upload) esse arquivo para na pasta 192.168.10.233/opt/srvweb/atualiza (Navegar entre as pastas que se abrirá a esqueda)
4. Navegar através do terminal até a pasta /opt/srvweb/atualiza
5. Executar o script de deploy com o comando abaixo:
 ```
 ./atualiza_protocolo.sh
 ./atualiza_fiscal.sh
 ```
* Obs.: caso de falha no deploy executar comando  **killall java** para matar processos.

6. Acessar o endereço http://192.168.10.233/ e verificar se o deploy obteve sucesso