---
title: Encerramento Compulsório
description: Executar encerramento compulsório localmente
published: true
date: 2020-04-29T02:12:29.324Z
tags: 
---

# Encerramento Compulsório na Máquina Local

Para testar o encerramento compulsório localmente é necessário realizar a seguinte configuração no standalone.xml ( pasta do wildfly standalone\configuration)

```java
 <system-properties>
        <property name="br.com.neainformatica.nfseletronica.schedule.ProcessoEncerramentoCompulsorio" value="true"/>
</system-properties>
```
No banco, na tabela agendamento, será necessário alterar o parâmetro de "Encerramento diário as 21h" para a expressão: 0/5 * * * * ? *
