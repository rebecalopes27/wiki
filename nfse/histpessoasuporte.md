---
title: Acesso de Usuário Suporte
description: Alterações realizadas para que usuário suporte acesse o sistema do Nota Fiscal
published: true
date: 2020-06-04T21:17:28.603Z
tags: suporte, acesso
---

# Cadastro de usuário SUPORTE

* Alterações foram realizadas visando a melhoria no sistema quanto a nível de segurança e auditoria.

* Anteriormente o acesso ao sistema de Nota Fiscal era realizado com o login padrão para todos **SUPORTE** e senha dia. Com as alteraçãoes realizadas no sistema, o acesso para usuários da empresa, será realizado via CPF e senha pessoal.

* O cadastro de usuários de funcionários da N&A Informática será realizado via satsync, ou seja, serão cadastrados via banco de dados. Dessa forma sempre que um funcionário novo ingressar na empresa, liberando acessos aos sistemas, libera também acesso ao Nota Fiscal. E caso funcionário seja desligado, automáticamente os acessos aos sistemas serão removidos.

# Comportamento do Sistema

* O Nota Fiscal atualmente (06/2020) não trabalha com a tabela "na_usuario" para atenticação de usuários no sistema, a tabela "pessoa" é usada para isso. Portanto, o sistema verifica se há usuários com nível 32/64 na tabela "na_usuario" e cria novos usuários na tabela "pessoa" vinculando na tabela "pessoaperfil" o id da pessoa e o perfil de usuário suporte ou administrador. Caso não exista mais o usuário na tabela "na_usuario", ele juntamente com o perfil, são removidos da tabela pessoa.

# Nível de Usuário

* Na tabela "na_usuario" o campo nivelusuario identifica qual o nível de acesso o usuário possui dentro do sistema. Nivel de Acesso igual a 32 é o nível SUPORTE, e o nivel de acesso 64 é o nivel de usuário ROOT, mas no Nota Fiscal equivale ao ADMIN.

## Nível 32 - O que pode ou não fazer











