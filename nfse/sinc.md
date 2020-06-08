---
title: Sincronismo 
description: Sincronismo dos sistemas SAT e Nota Fiscal
published: true
date: 2020-06-08T12:37:32.827Z
tags: sat, sincronismo, nota
---

# Sincronismo

* O sincronismo tem por objetivo sincronizar informações que são, em geral, cadastradas no SAT e precisam ser atualizadas também no Nota Fiscal. Informações como: uma nova empresa cadastrada no SAT e seus respectivos dados, como também baixa de débitos. Após indicar na empresa que os dados deverão sincronizar com o sistema do Nota Fiscal, esses dados serão automáticamente sincronizados.


# Executar sincronismo na máquina local

* Para executar o sincronismo na máquina local será nescessário realizar algumas configurações. Lembrando que executamos simultâneamente duas aplicações: **atualizaNF-Server** e **atualizaNF-Clien**t, uma depende da outra pra funcionarem corretamente. Mas antes é necessário entender quais bancos serão utilizados para realizar o sincronismo.

## Banco de dados para conexão

* Para começar tenha em mente que os bancos necessários para realizar o procedimento de sincronismo são:

- **Banco do antigo sistema ISS Web**
- **Banco do SAT ( Sistema de administração Tributária)** 
- **Banco do Nota Fiscal**

* Esses três bancos serão necessário estarem o mais atualizados possível. Após atualizar, pode-se começar a próxima etapa de configuração

## Conexão do Datasource

* A configuração do *DataSource* para executar o sincronismo deve ser feita no **WildFly 15.0.0**. As principais configurações serão:
<br/>
   - **Banco do SAT**: /satSincDS 
   - **Banco ISS**: /issDS
   - **Banco do NOTA**: /atualizaNF-ServerDS
   - **Banco do SAT:** /atualizaNF-ClientDS
* Segue abaixo um exemplo de configuração:

> Conexão atualizaNF-ClientDS
{.is-info}

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

> Conexão atualizaNF-ServerDS
{.is-info}

```Java
<datasource jndi-name="java:/atualizaNF-ServerDS" pool-name="atualizaNF-ServerDS"
		jta="true" use-ccm="false" enabled="true">
		<connection-url>jdbc:postgresql://192.168.10.233:5432/ms_treslagoas_nfse</connection-url>
		<driver-class>org.postgresql.Driver</driver-class>
		<driver>postgresql-9.4.1212.jar</driver>
		<security>
			<user-name>postgres</user-name>
			<password>n519631a*</password>
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
```

> Conexão satSincDS
{.is-info}

```Java
<datasource	jndi-name="java:/satSincDS" pool-name="satSincDS"
		jta="false" use-ccm="false" enabled="true">
		<connection-url>jdbc:firebirdsql:192.168.10.150/3025:D:/Bases/TresLagoas/Tributacao.fdb?lc_ctype=ISO8859_1</connection-url>
		<driver>jaybird-full-2.2.5.jar</driver>
		<security>
			<user-name>****</user-name>
			<password>****</password>
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
> Conexão issDS
{.is-info}

```Java
	jta="false" use-ccm="false" enabled="true">
		<connection-url>jdbc:firebirdsql:192.168.10.233:/dados/firebird/ms_treslagoas_iss.fdb?lc_ctype=ISO8859_1</connection-url>
		<driver>jaybird-full-2.2.5.jar</driver>
		<security>
			<user-name>****</user-name>
      <password>****</password>
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

## Configurações nos Bancos de Dados
* As próximas configurações serão realizadas nos parâmetros de banco, do SAT e Nota Fiscal.


**1. Banco de dados SAT**
* No banco de dados do SAT (Firebird), na tabela **na_parametro_valor**, nesse banco será configurado as conexões do *atualizaNF-ClientDS*. Realizar o select para consultar os parâmatros, será apresentado algo assim:

![parametro_nfclient.png](/imagens/parametro_nfclient.png){.align-center}


* Será necessário configurar dois parâmetros, que podem ser identificados pela coluna de nome **"chave**". O primeiro parâmetro será o **IP_MAQUINA_CLIENTE**, esse IP deverá ser alterado para o IP local da sua máquina (IPCONFIG para verificar o IP). 

> **Cuidado:** caso haja VM na mesma máquina, talvez seja necessário desinstalar.
{.is-warning}

* O segundo parâmetro a ser configurado será o **URL_API_SERVER**, nele configurar o seguinte parâmetro: **http://localhost:17170/atualizaNF-Server/api**

Algumas observações quanto ao parâmetro **URL_API_SERVER**

1.  Este parâmetro é utilizado pela API para criar a URL de envio/recebimento de remessa para sincronizar. Portanto, como o projeto esta sendo utilizado localmente, será necessário passar **localhost**. 

2. A porta poderá ser qualquer uma, menos a porta **8080**, pois essa é utilizada pelo banco do Nota Fiscal. No exemplo acima utiliza-se a porta alta **17170**. 

3. A parte final da URL, identifica qual "atualiza" estamos querendo conectar, no caso o autualizaNF-Server/api

![server.png](/imagens/server.png){.align-center}

> **IMPORTANTE**: É necessário na configuração do servidor, para rodar a aplicação do  autualizaNF-Server alterar o contexto da url passando o localhost e porta alterada. Também é necessário alterar a Port Offset para 9090.
{.is-danger}

**2. Banco de dados Nota Fiscal**

* No banco de dados do Nota Fiscal (PostgreSQL), na tabela **na_parametro_valor**, nesse banco será configurado as conexões do *atualizaNF-ServerDS*. Realizar o select para consultar os parâmatros, será apresentado algo assim: 

![parametro_nfserver.png](/imagens/parametro_nfserver.png){.align-center}

* Será necessário configurar três parâmetros, que podem ser identificados pela coluna de nome **"chave**". O primeiro parâmetro será o **IP_MAQUINA_CLIENTE**, esse IP deverá ser alterado para o IP local da sua máquina (IPCONFIG para verificar o IP).

* O segundo parâmetro será o **URL_API_CLIENT**, nele será configurado o seguinte parâmetro: **http://localhost:8080/atualizaNF-Client/api**

* O terceiro parâmetro será o **URL_API_SERVER** nele será configurado o seguinte parâmetro: **http://localhost:17170/atualizaNF-Server/api**

Após todas as configurações terem sido executadas, será necessário subir  os dois projetos. Startar ambos quase que no mesmo momento, ou o atualizaNF-Server primeiro e depois atualizaNF-Client.

Se nenhum erro ocorrer (esperamos que não) pode-se testar o sincronismo relizando alguma modificação no cadastro da empresa no SAT, sincronizar os dados pelo atualizaNF-Client ou pelo atualizaNF-Server, ao consultar no banco do nota fiscal a informação deverá ter siso incluida/alterada nele também.

> OBS: Para um devido funcionamento do sistema quando em testes, alterar o parametro na tabela na_agendamento (sem schema) - esse parâmetro só existe quando subir rodar a aplicação do atualizaNF-Server,  da tarefa relacionada com sincronismo. Essa tarefa é disparada a cada 5 segundos, se alterar o campo "ativo" para "N" a tarefa não será mais executada concomitantemente com os testes em máquina local.
{.is-danger}


# Acesso externo ao atualizaNF-Server

* Os usários do sistema de Nota Fiscal, com perfil PREFEITURA, geralmente ao alterar/incluir dados em uma empresa no SAT, forçam o sincronismo por dentro do Nota Fiscal. Pode ocorrer de o usuário não conseguir acessar, isso acontece porque ele precisa ter sido cadastrado e autorizado dentro do próprio sistema atualizaNF-Server.

