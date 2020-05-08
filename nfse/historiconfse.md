---
title: Histórico Alteração
description: Histórico de Alterações Importantes no código do NFSe - Encerramento Compulsório
published: true
date: 2020-05-08T18:25:46.535Z
tags: encerramento, alterações, histórico
---

# Encerramento Compulsório

* Problema referente a duplicação de Notas no ISS que ocasionava a duplicação também no SAT. (Meses 12/01/02/03 e 04)

> O que acasionou tal problema foi na Classe MesAno, o equals e hash foram apagados e na Amazon a instância de homologação apontava a job de encerramento para o banco de produção do ISS.

* Para realizar o cancelamentos dos débitos indevidos no SAT foram feitos os procedimentos descritos nos passos abaixo:

# Passo 1

* Localizado todos os lançamentos no SAT por um determinado periodo

````SQL
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
  AND COALESCE(LDP.COD_TIPO_BAIXA, 0) = 0
  AND LD.COD_LANCAMENTO STARTING '1' /*SERIA INTERESSANTE CRIAR UM CAMPO NA LANCTO_DEBITO PARA IDENTIFICAR SE O LANCAMENTO VEIO DO NOTA OU NAO*/
ORDER BY 1, 2, 3, 4
````

# Passo 2

* Localizado no banco do nota todos os lançamentos proprios e retidos do mesmo periodo

```SQL
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
```

# Passo 3 

* Localizando ambas colunas de lançamentos e comparando utilizando o excel

```SQL
Coluna 2 -> lançamentos do SAT
Coluna 1 -> lançamentos do Nota

coluna3-> formula usada =SEERRO(PROCV(linhaColuna2;todoIntervaloDaColuna1;1;0);"Indevido")
```
> Localizado todos os lançamentos que estão no SAT e que não estão no Nota

# Passo 4 

* Verificado todos esses lançamentos encontrados no SAT, para certificar de não estarem presentes em nenhum movimento

```SQL
select * from nfse.movimentomensal m
where m.cod_lancamento_iss_retido in (LISTA DE LANÇAMENTOS)

select * from nfse.movimentomensal m
where m.cod_lancamento_iss_proprio in (LISTA DE LANÇAMENTOS)
````

# Passo 5 
* No Banco do SAT foi feito update de cancelando em todos esses lançamentos

```SQL
UPDATE LANCTO_DEBITO_PARCELA LDP
SET LDP.PARCELA_CANCELADA = 1
WHERE COALESCE(LDP.COD_TIPO_BAIXA, 0) = 0
AND LDP.COD_LANCAMENTO IN ('LISTA DE LANÇAMENTOS')
```

# Passo 6

* No banco do ISS feito delete de todas essas declarações e seus vínculos

# Passo 7

* Localizado as declarações através dos lançamentos indevidos

```SQL
select t10.campo5 || ','
from tabela10 t10
left join tabela12 t12 on t12.campo2 = t10.campo1
where t12.campo19 in('LISTA DE LANÇAMENTOS')
```

# Passo 8

* Uma última verificação pegando o número dessas declarações e verificadno se não estão presentes em nenhum movimento

```SQL
select * from nfse.movimentomensal m
where m.numerodeclaracao in (LISTA DE DECLARAÇÕES)
```

# Passo 9

* Se não foi localizado nenhuma declaração, foi deletado no banco do ISS as declarações indevidas:

> Começando pela tabela 10

```SQL
delete from tabela10
where campo5 in (LISTA DE DECLARAÇÕES)
```

> TABELA 26 notas canceladas constantes na declaraçao

```SQL
delete from tabela26
where campo1 in (LISTA DE DECLARAÇÕES)
```

> TABELA 3 notas emitidas (porém não tem chave com a TABELA6)

```SQL
delete from tabela3 
where DECLARACAO_ID in (LISTA DE DECLARAÇÕES) 
```

> TABELA 5 notas recebidas

```SQL
delete from tabela5
where DECLARACAO_ID in (LISTA DE DECLARAÇÕES)
```
