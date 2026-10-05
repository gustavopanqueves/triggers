# triggers
---
atividade1 

***MYSQL***
```mysql
CREATE TABLE produtos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100),
    quantidade INT
);

CREATE TABLE historico_estoque (
    id INT PRIMARY KEY AUTO_INCREMENT,
    produto_id INT,
    quantidade_antiga INT,
    quantidade_nova INT,
    data_alteracao DATETIME
);

DELIMITER //

CREATE TRIGGER registrar_alteracao_estoque
AFTER UPDATE
ON produtos
FOR EACH ROW
BEGIN

    INSERT INTO historico_estoque (
        produto_id,
        quantidade_antiga,
        quantidade_nova,
        data_alteracao
    )
    VALUES (
        NEW.id,
        OLD.quantidade,
        NEW.quantidade,
        NOW()
    );

END //

DELIMITER ;

INSERT INTO produtos (nome, quantidade) VALUES
("MAMÃO", 1),
("SABÃO EM PÓ", 2);

SELECT * FROM produtos;

UPDATE produtos
SET quantidade = 4
WHERE ID = 1;

UPDATE produtos
SET quantidade = 7
WHERE ID = 1;

SELECT * FROM historico_estoque;
```
