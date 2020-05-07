---
title: Histórico Alteração
description: Histórico de Alterações Importantes no código do NFSe - Encerramento Compulsório
published: true
date: 2020-05-07T13:29:23.820Z
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