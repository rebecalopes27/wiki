---
title: Serviços Web Integração  via WebService (SOAP) Prefeitura de Dourados
description: Integração com os dados econômicos 
published: true
date: 2020-08-11T12:47:11.367Z
tags: webservice, dourados, integração
---

# Serviços Web Integração  via WebService (SOAP) Prefeitura de Dourados


- Prefeitura de Dourados não utiliza nosso módulo Fiscal. Portanto as informações de empresas se possuem algum débito economico em aberto são buscados via webservice (API SOAP) , que a empresa Nota Control nos fornece.

### WEB ATENDIMENTO - IMOBILIARIO:

- Endereço Inconsistente nao emite certidão, por exemplo: Se o contribuinte não tiver rua ou bairro ou numero ou cpf/cnpj não poderá emitir certidão negativa.

- Se tiver um parcelamento ativo(parcalmento de débitos) não poderá emitir certidão negativa

- Debitos em abertos NÃO vencidos, certidão será emitida normalmente
 
- Nenhum débito, certidão será emitida normalmente




###  SERVIÇOS WEB / Integração com Nota Control -  CPF/CNPJ

- O sitema verifica se há debitos vinculados(BICs) ao CPF/CNPJ, se houver debitos vencidos nao sera emitida a certidão

- Para Dourados existe um parametros no banco do SAT que esta configurado como "SIM" que Permite que certidões negativas imobiliarias sejam emitidas mesmo 
havendo débitos do exercício em aberto, desde que NÃO estejam vencidos.

- Um dos Proprietários/Sócios do cadastro Possuem débitos vencidos, não será emitida a certidão

Por último, para uma verificação melhor de como o sistema se comporta com relação aos dados economicos que a Nota Control nos provê, e que não possuimos cadastro no SAT,  seria melhor o cliente nos fornecer um CNPJ que conste débitos economicos. Mas o sistema no geral válida o seguinte:

 - Cadastros precisam estar com situação 2 (Ativo)
 -  Nenhum dos cadadastro pode possuir débitos
 -  Nenhum dos cadadastro pode possuir débitos EM DIA
 
### Link WSDL

http://www.issnetonline.com.br/webserviceIntegracao/IntegracaoCertidaoDourados/WSCertidaoNegativa.asmx?WSDL

### Link Orientaçõs gerais para emissão de Certidão Negativa - Nota Control

http://www.issnetonline.com.br/webserviceIntegracao/IntegracaoCertidaoDourados/WSCertidaoNegativa.asmx

