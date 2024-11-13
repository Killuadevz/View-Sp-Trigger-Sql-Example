## Aula 06/11/2024


## View 1 
```sql
CREATE VIEW cidades AS SELECT pais_id, pais FROM pais;
SELECT * FROM cidades LIMIT 3;
```

## View 2 
```sql
CREATE VIEW  aluguel AS SELECT aluguel_id , data_de_devolucao FROM aluguel;
SELECT * FROM aluguel ORDER BY data_de_devolucao ASC;
SELECT * FROM aluguel LIMIT 100;
```

## View 3 
```sql
CREATE VIEW  ator AS SELECT ator_id , primeiro_nome FROM ator;
SELECT * FROM ator ORDER BY primeiro_nome DESC;
SELECT * FROM ator LIMIT 100;
```

## SP 1
```sql
DELIMITER //
CREATE PROCEDURE FINDBYNAME (in id int)
BEGIN 
SELECT C.NOME, COUNT(F.TITULO) AS QTD_FILMES
FROM CATEGORIA C
JOIN FILME_CATEGORIA FC ON C.CATEGORIA_ID = FC.CATEGORIA_ID
JOIN FILME F ON F.FILME_ID = FC.FILME_ID
WHERE F.CLASSIFICACAO = 'G'
GROUP BY C.NOME;
END //
DELIMITER ;

CALL FINDBYNAME(1);

```
## SP 2

```sql

DELIMITER //
CREATE PROCEDURE FIND400 (in id int)
BEGIN 
SELECT ANO_DE_LANCAMENTO, COUNT(TITULO) AS QTD_FILMES
FROM FILME
GROUP BY ANO_DE_LANCAMENTO
HAVING COUNT(TITULO) > 400;
END //
CALL FIND400(1);
```

## SP 3
```sql
DELIMITER //
CREATE PROCEDURE FINDCITY (in id int)
BEGIN 
SELECT P.PAIS, COUNT(C.CIDADE) AS QTD_CIDADES
FROM PAIS P
JOIN CIDADE C ON P.PAIS_ID = C.PAIS_ID
GROUP BY P.PAIS
ORDER BY QTD_CIDADES DESC;
END //
CALL FINDCITY(1);
```

## Trigger 1
```sql
DELIMITER $$
CREATE TRIGGER after_update_loja
AFTER UPDATE ON LOJA
FOR EACH ROW
BEGIN
INSERT INTO log_updates (descricao, data_atualizacao)
VALUES ('Loja atualizada', NOW());
END $$
DELIMITER ;
```

## Trigger 2

```sql
DELIMITER $$
CREATE TRIGGER after_update_idioma
AFTER UPDATE ON idioma
FOR EACH ROW
BEGIN
INSERT INTO log_updates (descricao, data_atualizacao)
VALUES ('idioma atualizada', NOW());
END $$
DELIMITER ;
```

##  Trigger 3
```sql
DELIMITER $$
CREATE TRIGGER after_update_inventario
AFTER UPDATE ON inventario
FOR EACH ROW
BEGIN
INSERT INTO log_updates (descricao, data_atualizacao)
VALUES ('idioma atualizada', NOW());
END $$
DELIMITER ;
```
