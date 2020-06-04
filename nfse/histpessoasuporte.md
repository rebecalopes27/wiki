---
title: Acesso de Usuário Suporte
description: Alterações realizadas para que usuário suporte acesse o sistema do Nota Fiscal
published: true
date: 2020-06-04T21:28:42.300Z
tags: suporte, acesso
---

# Cadastro de usuário SUPORTE

* Alterações foram realizadas visando a melhoria no sistema quanto ao nível de segurança e auditoria.

* Anteriormente o acesso ao sistema de Nota Fiscal era realizado com o login padrão para todos **SUPORTE** e senha dia. Com as alteraçãoes realizadas no sistema, o acesso para usuários da empresa, será realizado via CPF e senha pessoal.

* O cadastro de usuários de funcionários da N&A Informática será realizado via satsync, ou seja, serão cadastrados via banco de dados. Dessa forma sempre que um funcionário novo ingressar na empresa, liberando acessos aos sistemas, libera também acesso ao Nota Fiscal. E caso funcionário seja desligado, automáticamente os acessos aos sistemas serão removidos.

# Comportamento do Sistema

* O Nota Fiscal atualmente (06/2020) não trabalha com a tabela "na_usuario" para atenticação de usuários no sistema, a tabela "pessoa" é usada para isso. Portanto, o sistema verifica se há usuários com nível 32/64 na tabela "na_usuario" e cria novos usuários na tabela "pessoa" vinculando na tabela "pessoaperfil" o id da pessoa e o perfil de usuário suporte ou administrador. Caso não exista mais o usuário na tabela "na_usuario", ele juntamente com o perfil, são removidos da tabela pessoa.

# Nível de Usuário

* Na tabela "na_usuario" o campo nivelusuario identifica qual o nível de acesso o usuário possui dentro do sistema. Nivel de Acesso igual a 32 é o nível SUPORTE, e o nivel de acesso 64 é o nivel de usuário ROOT, mas no Nota Fiscal equivale ao ADMIN.

## Nível SUPORTE

* Atualmente o usuário SUPORTE só poderá acessar o sistema em **modo consulta**, não podendo realizar nenhuma alteração no sistema. Isso apenas em PRODUÇÂO, mas em HOMOLOGAÇÂO o usuário suporte poderá realizar qualquer procedimento.

* Caso o usuário SUPORTE precise realizar urgentemente algum procedimento no sistema, será necessário que um usuário com nível ADMIN acesse o sistema, pois usuário ADMIN não acessa o sistema em modo consulta, sendo  possivel realizar qualquer procedimento no sistema. Ou alterar via banco de dados o perfil do usuário de SUPORTE para ADMIN.

## Nível ADMIN

* O nível admin foi adicionado para poder realizar qualquer procedimento no sistema, todos os CRUDS são permitidos a esse usuário. Ele pode acessar qualquer pessoa no sistema, adicionar qualquer perfil, inclusive de SUPORTE, e remover qualquer pessoa e perfil. Para este usuário o sistema tanto em PRODUÇÃO como HOMOLOGAÇÂO não será aberto como consulta.












