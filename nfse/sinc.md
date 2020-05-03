---
title: Sincronismo - Autorização de Usuário 
description: Acesso ao sincronismo (atualizaNF-Client)
published: true
date: 2020-04-29T02:09:43.202Z
tags: 
---

# Sincronismo
No sistema do Nota Fiscal existe a opção de”Forçar Sincronismo” para isso é necessário que o usuário logado tenha o cadastro no AtualizaNF-Server
Link: https://web.neainformatica.com.br/pmtlsatualizaNF-Server/ 

## Subir o Serviço na máquina local

Para subir o serviço do atualizaNF-Server, em sua máquina local utilizar Widfly 15.0.0.
Verificar também se seu dataSource se enontra corretamente configurado, conforme exemplo abaixo:

```java
<datasource	jndi-name="java:/satSincDS" pool-name="satSincDS"
		jta="false" use-ccm="false" enabled="true">
		<connection-url>jdbc:firebirdsql:192.168.10.233/3050:/opt/dados/ms_treslagoas_sat.fdb?lc_ctype=ISO8859_1</connection-url>
		<driver>jaybird-full-3.0.6.jar</driver>
		<security>
			<user-name>USUARIO DO BANCO DE DADOS</user-name>
			<password>senha do banco de dados</password>
		</security>
		<validation>
			<validate-on-match>false</validate-on-match>
			<background-validation>false</background-validation>
		</validation>
		<statement>
			<share-prepared-statements>false</share-prepared-statements>
		</statement>
	</datasource>
	
	<datasource jndi-name="java:/atualizaNF-ServerDS" pool-name="atualizaNF-ServerDS"
		jta="true" use-ccm="false" enabled="true">
		<connection-url>jdbc:postgresql://192.168.10.233:5432/ms_treslagoas_nfse</connection-url>
		<driver-class>org.postgresql.Driver</driver-class>
		<driver>postgresql-9.4.1212.jar</driver>
		<security>
			<user-name>USUARIO DO BANCO DE DADOS</user-name>
			<password>senha do banco de dados</password>
		</security>
    <validation>
			<validate-on-match>true</validate-on-match>
			<background-validation>false</background-validation>
			<check-valid-connection-sql>SELECT 1</check-valid-connection-sql>
		</validation>
		<timeout>
			<blocking-timeout-millis>30000</blocking-timeout-millis>
			<idle-timeout-minutes>1</idle-timeout-minutes>
		</timeout>
		<statement>
			<share-prepared-statements>false</share-prepared-statements>
		</statement>
	</datasource>
	<datasource	jndi-name="java:/issDS" pool-name="issDS"
		jta="false" use-ccm="false" enabled="true">
		<connection-url>jdbc:firebirdsql:192.168.10.233/3050:/opt/dados/ms_treslagoas_iss.fdb?lc_ctype=ISO8859_1</connection-url>
		<driver>jaybird-full-3.0.6.jar</driver>
		<security>
			<user-name>USUARIO DO BANCO DE DADOS</user-name>
			<password>senha do banco de dados</password>
		</security>
		<validation>
			<validate-on-match>false</validate-on-match>
			<background-validation>false</background-validation>
		</validation>
		<statement>
			<share-prepared-statements>false</share-prepared-statements>
		</statement>
	</datasource>
```
