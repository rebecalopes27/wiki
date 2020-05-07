---
title: Histórico Alteração
description: Histórico de Alterações Importantes no código do NFSe - Encerramento Compulsório
published: true
date: 2020-05-07T13:40:05.870Z
tags: encerramento, alterações, histórico
---

# Encerramento Compulsório

* Problema referente a duplicação de Notas no ISS que ocasionava a duplicação também no SAT

Para fazer o cancelamentos dos débitos indevidos no SAT foram feitos os procedimentos abaixo:

# **1. Localizei todos os lançamentos no SAT por um determinado periodo**

SELECT
  LD.EXERCICIO,
  LD.COD_IMPOSTO,
  LD.COD_LANCAMENTO,
  LDP.PARCELA,
  LDP.VALOR_ORIGINAL,
  IIF(COALESCE(LDP.COD_TIPO_BAIXA, 0) = 0 AND COALESCE(LDP.PARCELA_CANCELADA, 0) = 0, 'Pendente', 'Pago') AS SITUACAO_TRIBUTOS
  FROM LANCTO_DEBITO LD
    LEFT JOIN LANCTO_DEBITO_PARCELA LDP
      ON LDP.COD_LANCAMENTO = LD.COD_LANCAMENTO
WHERE COALESCE(LD.COD_LANCAMENTO, '') <> ''
  AND LD.TIPO_ORIGEM = 2
  AND LD.EXERCICIO >= 2020
  AND LD.COD_IMPOSTO IN ('201','203')
  AND COALESCE(LDP.PARCELA_CANCELADA, 0) = 0
  AND LD.COD_LANCAMENTO STARTING '1' /*SERIA INTERESSANTE CRIAR UM CAMPO NA LANCTO_DEBITO PARA IDENTIFICAR SE O LANCAMENTO VEIO DO NOTA OU NAO*/
ORDER BY 1, 2, 3, 4

# **2. Localizei no banco do nota todos os lançamentos proprios e retidos do mesmo periodo**

select m.cod_lancamento_iss_proprio AS LANCAMENTO_NOTA
from nfse.movimentomensal m
where m.anocompetencia >= 2020
and m.cod_lancamento_iss_proprio is not NULL
and m.situacao <> 'C'

union

select m.cod_lancamento_iss_retido AS LANCAMENTO_NOTA
from nfse.movimentomensal m
where m.anocompetencia >= 2020
and m.cod_lancamento_iss_retido is not NULL
and m.situacao <> 'C'

# **3. Peguei ambas colunas de lançamentos e comparei utilizando o excel**

Coluna 2 -> lançamentos do SAT
Coluna 1 -> lançamentos do Nota

coluna3-> formula usada =SEERRO(PROCV(linhaColuna2;todoIntervaloDaColuna1;1;0);"Indevido")

localizei todos os lançamentos que estão no SAT que não estão no Nota

# **4. Testei por desencargo todos esses lançamentos encontrados no SAT, para verificar se não estão presentes em nenhum movimento**#

select * from nfse.movimentomensal m
where m.cod_lancamento_iss_retido in (LISTA DE LANÇAMENTOS)

select * from nfse.movimentomensal m
where m.cod_lancamento_iss_proprio in (LISTA DE LANÇAMENTOS)

# **5. Fui no Banco do SAT e rodei um update cancelando todos esse lançamentos**

UPDATE LANCTO_DEBITO_PARCELA
SET PARCELA_CANCELADA = 1
WHERE COD_LANCAMENTO IN ('LISTA DE LANÇAMENTOS')

# **6. Fui para o banco do ISS para deletar todas essas declarações e seus vinculos**

# **7. Localizei as declarações através dos lançamentos indevidos**

select t10.campo5 || ','
from tabela10 t10
left join tabela12 t12 on t12.campo2 = t10.campo1
where t12.campo19 in('LISTA DE LANÇAMENTOS')'

# **8. Mais uma vez por desencargo , pego o numero dessas declarações e verifico se não estão presentes em nenhum movimento**

select * from nfse.movimentomensal m
where m.numerodeclaracao in (LISTA DE DECLARAÇÕES)

# **9. Se não localizou nenhuma declaração, vou deletar no banco do iss as declarações indevidas**

->Começando pela tabela 10

delete from tabela10
where campo5 in (LISTA DE DECLARAÇÕES)

->TABELA 26 notas canceladas constantes na declaraçao

delete from tabela26
where campo1 in (LISTA DE DECLARAÇÕES)

->TABELA 3 notas emitidas    (porem nao tem chave com a tabela6)

delete from tabela3 
where DECLARACAO_ID in (LISTA DE DECLARAÇÕES)  

->TABELA 5 notas recebidas
delete from tabela5
where DECLARACAO_ID in (LISTA DE DECLARAÇÕES)

