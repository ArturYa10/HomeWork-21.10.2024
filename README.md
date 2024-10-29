   -- Dz
    
    CREATE TABLE goods (
    id INT PRIMARY KEY,
    title VARCHAR(30) NOT NULL,
    quantity INT CHECK (quantity > 0),
    instock CHAR(1) CHECK (instock IN ('Y', 'N'))
);


INSERT INTO goods (id, title, quantity, instock) VALUES (1, 'Велосипед', 2, 'Y');
INSERT INTO goods (id, title, quantity, instock) VALUES (2, 'Скейт', 4, 'Y');
INSERT INTO goods (id, title, quantity, instock) VALUES (3, 'Самокат', 2, 'Y');
INSERT INTO goods (id, title, quantity, instock) VALUES (4, 'Сноуборд', 7, 'N');
INSERT INTO goods (id, title, quantity, instock) VALUES (5, 'Санки', 1, 'Y');
INSERT INTO goods (id, title, quantity, instock) VALUES (6, 'Коньки', 3, 'N');
INSERT INTO goods (id, title, quantity, instock) VALUES (7, 'Ролики', 5, 'Y');
INSERT INTO goods (id, title, quantity, instock) VALUES (8, 'Гироскутер', 6, 'Y');
INSERT INTO goods (id, title, quantity, instock) VALUES (9, 'Лыжи', 2, 'N');
INSERT INTO goods (id, title, quantity, instock) VALUES (10, 'Квадроцикл', 1, 'Y');


-- Dz 2

CREATE TABLE goods_2 (
    id INT PRIMARY KEY,
    title VARCHAR(30) NOT NULL,
    quantity INT CHECK (quantity > 0),
    price INT NOT NULL,
    in_stock CHAR(1) CHECK (in_stock IN ('Y', 'N'))
);


INSERT INTO goods_2 (id, title, quantity, price, in_stock) VALUES (1, 'Тюбинг', 5, 1000, 'Y');
INSERT INTO goods_2 (id, title, quantity, price, in_stock) VALUES (2, 'Санки', 2, 1500, 'Y');
INSERT INTO goods_2 (id, title, quantity, price, in_stock) VALUES (3, 'Снегокат', 2, 900, 'Y');
INSERT INTO goods_2 (id, title, quantity, price, in_stock) VALUES (4, 'Сноуборд', 7, 700, 'N');
INSERT INTO goods_2 (id, title, quantity, price, in_stock) VALUES (5, 'Клюшка', 8, 300, 'Y');
INSERT INTO goods_2 (id, title, quantity, price, in_stock) VALUES (6, 'Коньки', 3, 350, 'N');
INSERT INTO goods_2 (id, title, quantity, price, in_stock) VALUES (7, 'Форма', 9, 450, 'Y');
INSERT INTO goods_2 (id, title, quantity, price, in_stock) VALUES (8, 'Гироскутер', 6, 5000, 'Y');
INSERT INTO goods_2 (id, title, quantity, price, in_stock) VALUES (9, 'Лыжи', 3, 1200, 'N');
INSERT INTO goods_2 (id, title, quantity, price, in_stock) VALUES (10, 'Квадроцикл', 1, 10000, 'Y');


SELECT title FROM goods
UNION ALL
SELECT title FROM goods_2;

SELECT title FROM goods
UNION
SELECT title FROM goods_2;

SELECT 
    g.id,
    g.title,
    g.quantity,
    COALESCE(g2.price, 0) AS price,
    g.instock AS in_stock
FROM 
    goods AS g
LEFT JOIN 
    goods_2 AS g2 
ON 
    g.title = g2.title

UNION ALL

SELECT 
    g2.id,
    g2.title,
    g2.quantity,
    g2.price,
    g2.in_stock
FROM 
    goods_2 AS g2
WHERE 
    g2.title NOT IN (SELECT title FROM goods);
