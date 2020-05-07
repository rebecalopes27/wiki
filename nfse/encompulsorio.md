---
title: Encerramento Compulsório
description: Executar encerramento compulsório localmente
published: true
date: 2020-05-07T02:42:20.089Z
tags: encerramento
---

# Encerramento Compulsório na Máquina Local

Para testar o encerramento compulsório localmente é necessário realizar a seguinte configuração no standalone.xml ( pasta do wildfly standalone\configuration)

```java
 <system-properties>
        <property name="br.com.neainformatica.nfseletronica.schedule.ProcessoEncerramentoCompulsorio" value="true"/>
</system-properties>
```
No banco, na tabela agendamento, será necessário alterar o parâmetro de "Encerramento diário as 21h" para a expressão: 0/5 * * * * ? *

# Como funciona o Encerramento Compulsório

* Funcionamento do encerramento compulsório - Passos

# Principais Classes e Métodos Responsáveis

