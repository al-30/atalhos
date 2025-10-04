Inner Join

```SQL
SELECT
    tab2.Protocolo,
    tab1.id,
    tab1.colunaB,
    tab1.IdStatus,
    tab1.IdProcesso,
    tab1.TipoPreSelecionado,
    tab1.Colocacao
FROM tabela1 tab1
INNER JOIN tabela2 tab2
    ON tab2.id = tab1.colunaB
WHERE tab1.IdProcesso = 2219
and tab2.Protocolo in (0000107741,1000046025)
ORDER BY tab1.Colocacao;
```

### Insert

Neste exemplo, foi realizada a combinacao do comando **Insert** com **Select**.
Insere na TabelaA, os registros filtrados pelo Select na TabelaB.

```SQL
INSERT INTO TabelaA (DATA, ColunaA, IdDaTabelaB, ColunaC)
SELECT GETDATE(), 0, id,6
FROM TabelaB
WHERE ColunaA =25;
```

### Update

```SQL
UPDATE Tabela SET colunaA = 0
WHERE Id IN (39606,39605,39351,39175);
```

### Select

```SQL
/*Filtro para a data atual*/
SELECT *
FROM Tabela
WHERE CAST(Data AS DATE) = CAST(GETDATE() AS DATE);

/*Pega os 100 primeiros com filtro para o dia anterior */
SELECT TOP (100) *
FROM Tabela
WHERE CAST(Data AS DATE) = CAST(DATEADD(DAY, -1, GETDATE()) AS DATE);
```
