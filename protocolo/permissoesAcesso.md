---
title: Permissões de usuários Protocolo
description: Descrição das permissões de usuários do sistema Protocolo
published: true
date: 2020-06-30T13:37:06.566Z
tags: protocolo, permissões, usuários
---

# Permissões de Usuários no PROTOCOLO

* | Operação | Classe e Método | Nível Critico
:------|:------|:------:|:------:| :------:
1 | Modo leitura | Usuário Suporte/Administrador não acessa modo leitura | -
2 | Processa Relatório | ProcessoRelatorioControllerinit() | <span style="color:green">1</span>
3 | Copia processos | SessionControllerisCopiaProcessos()| <span style="color:green">1</span>
4 | Recepciona guia de remessa | SessionControllerisRecepcionaGuiaDeRemessa() | <span style="color:red">5</span>