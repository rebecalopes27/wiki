---
title: Sincronismo - Autorização de Usuário 
description: Acesso ao sincronismo (atualizaNF-Client)
published: true
date: 2020-05-20T00:59:31.447Z
tags: 
---

# Sincronismo

* O sincronismo ter por objetivo sincronizar informações que são, em geral, cadastradas no SAT e precisam ser utilizadas também no Nota Fiscal. Informações como: nova empresa cadastrada no SAT (isso em Três Lagoas) e seus respectivos dados, ao indicar na empresa que os dados deverão sincronizar com NF, esses dados serão automáticamente sincronizados.


# Executar sincronismo na máquina local

* Para executar o sincronismo na máquina local será nescessário realizar algumas configurações.Mas antes é necessário entender quais bancos serão utilizados para realizar o sincronismo.

## Banco de dados para conexão

* Para começar tenha em mente que os bancos necessários para realizar o procedimento de sincronismo são:

- **Banco do antigo sistema ISS Web**
- **Banco do SAT ( Sistema de administração Tributária)** 
- **Banco do Nota Fiscal**

* Esses três bancos será necessário estar o mais atualizados possível. Após atualizar, pode-se começar a próxima etapa de configuração

## Conexão do Datasource

* A configuração do *DataSource* para executar o sincronismo deve ser feita no **WildFly 15.0.0**. As principais configurações serão:
<br/>
   - **Banco do SAT**: /satSincDS 
   - **Banco ISS**: /issDS
   - **Banco do NOTA**: /atualizaNF-ServerDS
   - **Banco do SAT:** /atualizaNF-ClientDS
* Segue abaixo um exemplo de configuração:


```Java
<datasource	jndi-name="java:/atualizaNF-ClientDS" pool-name="atualizaNF-ClientDS"
		jta="false" use-ccm="false" enabled="true">
		<connection-url>jdbc:firebirdsql:192.168.10.150/3025:D:/Bases/TresLagoas/Tributacao.fdb?lc_ctype=ISO8859_1</connection-url>
		<driver>jaybird-full-2.2.5.jar</driver>
		<security>
			<user-name>****</user-name>
			<password>*****</password>
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
> Conexão atualizaNF-ClientDS
{.is-info}







