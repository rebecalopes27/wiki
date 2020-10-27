---
title: Webservice
description: Webservice para comunicação entre sistemas
published: true
date: 2020-10-27T12:10:10.581Z
tags: webservice, xml, rps
---

# Webservice

*  O que é o Webservice

*"Webservice é uma solução utilizada na integração de sistemas e na comunicação entre aplicações diferentes. Com esta tecnologia é possível que novas aplicações possam interagir com aquelas que já existem e que sistemas desenvolvidos em plataformas diferentes sejam compatíveis.*" 

* Quando os clientes utilizam Webservice

Os clientes geralmente possuem sistema próprios para envio de RPS (Recibo Provisório de Serviços) e/ou enviar Notas Fiscais Elêtronicas, este último quando não utilizam o nosso sistema.Essa troca de informações é feita via arquivo XML assinado digitalmente, onde o contribuinte não terá a necessidade emitir suas Notas Fiscais on-line no site do município.

* Como é utilizado

Os clientes que decidem utilizar o webservice como meio de comunicação entre o nosso sistema, acessam o site do Nota Fiscal e baixam o "Manual do Contribuinte", nele estão especificados como realizar o envio.

# Classes e Métodos

* Classes são responsáveis pelo Webservice

* Métodos são responsáveis pelo Webservice

# Como Testar o Webservice Localmente

* Passos para o teste local no código
->é usado para o envio a aplicação webservice-client e o nota pra recepcionar as rps
  No webserice-client na classe Cliente.java configurar o caminho do wsdl e o método que vai ser testado.
  ![screenshot_19.png](/screenshot_19.png)
  
 ->No arquivo xmlTest.xml tem que inserir o xml que vai ser enviado, com as tags SoupUi não funcionou muito bem, tem que tirar as tags Soup para o arquivo ser enviado corretamente.
 
 Depois disso só dar um Run na classe Cliente.java , o nota tem que estar no ar.
 
Se o xml for enviado com successo a app retorna com uma mensagem com um numero de protocolo , se der algum erro ele tem retorna com o erro.

```
EnviarLoteRpsResposta xmlns="http://www.abrasf.org.br/nfse.xsd">
  <NumeroLote>10</NumeroLote>
  <DataRecebimento>2020-10-23T15:26:24</DataRecebimento>
  <Protocolo>558653</Protocolo>
</EnviarLoteRpsResposta>
```

Ao chegar no nota o arquivo vira um registro na tabela lotetransmissao, onde no nota precisa ser configurado para que o lote seje processado e convertido em nota fiscal.

Para configurar o nota acesse o arquivo standalone.xml e acrescente o seguinte trecho:

```
Logo abaixo do fim da tag (extension).

<system-properties>
        <property name="br.com.neainformatica.nfseletronica.schedule.ProcessoRemessaRps" value="true"/>
</system-properties>
```

Altera na tabela nfse.agendamento o valor de quanto tempo vai rodar as atualizações das rps , é usado o crow numeric 
hoje no banco ele esta pra rodar a cada 1 minuto 0 0/1 * * * ? *  

Configurando isso o nota vai executar as rotinas de conversão de rps.

Os métodos estão na classe servicosWebTools
  
  
  

* Passos para o teste local com Software SoapUI (Muito usado pelos clientes)

# Tag CDATA para teste com SoapUI
->Para envio de arquivos xml usando o SoapUI tem que se usar a tag CDATA
Ex: xml consulta

```
<?xml version="1.0" encoding="UTF-8"?>
<soap:Envelope
    xmlns:nfse="http://nfse.abrasf.org.br"
    xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Header/>
    <soap:Body>
        <nfse:ConsultarLoteRps>
            <ConsultarLoteRpsEnvio>
                <![CDATA[
				<ConsultarLoteRpsEnvio
                xmlns="http://www.abrasf.org.br/nfse.xsd"><Prestador><CpfCnpj><Cnpj>04311093001521</Cnpj></CpfCnpj><InscricaoMunicipal>103735</InscricaoMunicipal></Prestador><Protocolo>555071</Protocolo></ConsultarLoteRpsEnvio>]]>
            </ConsultarLoteRpsEnvio>
        </nfse:ConsultarLoteRps>
    </soap:Body>
</soap:Envelope>
```


# Identificar XML mal formatado





