# 📚 Aula 6: Consultas em Múltiplas Tabelas no PostgreSQL

## 🎯 Objetivo da Aula

Aprender a realizar **consultas que envolvem múltiplas tabelas** no **PostgreSQL**, utilizando relacionamentos entre tabelas e condições no `WHERE` para combinar dados de forma eficiente.

## 🛠️ Script de Criação do Banco (PostgreSQL)

```sql

-- =========================================================
-- TABELA: clientes
-- =========================================================

CREATE TABLE clientes (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    idade INT,
    cidade VARCHAR(100) NOT NULL
);

-- =========================================================
-- TABELA: produtos
-- =========================================================

CREATE TABLE produtos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    categoria VARCHAR(100) NOT NULL,
    preco NUMERIC(10,2) NOT NULL
);

-- =========================================================
-- TABELA: compras
-- =========================================================

CREATE TABLE compras (
    id SERIAL PRIMARY KEY,
    cliente_id INT NOT NULL,
    produto_id INT NOT NULL,
    quantidade INT NOT NULL CHECK (quantidade > 0), -- Este código gera verifica se a quantidade é acima de 0
    data_compra DATE NOT NULL,

    CONSTRAINT fk_compras_clientes
        FOREIGN KEY (cliente_id)
        REFERENCES clientes(id),

    CONSTRAINT fk_compras_produtos
        FOREIGN KEY (produto_id)
        REFERENCES produtos(id)
);

-- =========================================================
-- DADOS DE EXEMPLO
-- =========================================================

INSERT INTO clientes (nome, idade, cidade) VALUES
('Ana Fernandes', 28, 'São Paulo'),
('Bruno Lima', 35, 'Canoas'),
('Carla Souza', 22, 'Porto Alegre'),
('Diego Martins', 40, 'Salvador'),
('Eduarda Alves', 31, 'Canoas'),
('Felipe Rocha', 27, 'São Paulo'),
('Gabriela Costa', 45, 'Salvador'),
('Henrique Dias', 19, 'Porto Alegre');

INSERT INTO produtos (nome, categoria, preco) VALUES
('Notebook Gamer Nitro', 'Informática', 4500.00),
('Notebook Ultra Slim', 'Informática', 3200.00),
('Mouse Gamer RGB', 'Eletrônicos', 180.00),
('Teclado Mecânico', 'Eletrônicos', 350.00),
('Monitor 24 Polegadas', 'Eletrônicos', 1200.00),
('Gamepad 54', 'Games', 250.00),
('Camiseta Star Wars', 'Vestuário', 89.90),
('Camiseta Naruto', 'Vestuário', 79.90),
('SSD 1TB', 'Informática', 550.00),
('Headset Gamer', 'Eletrônicos', 420.00);

INSERT INTO compras (cliente_id, produto_id, quantidade, data_compra) VALUES
(1, 1, 1, '2025-01-10'), -- Ana -> Notebook Gamer Nitro
(1, 7, 2, '2025-02-15'), -- Ana -> Camiseta Star Wars
(1, 6, 1, '2025-02-20'), -- Ana -> Gamepad 54

(2, 3, 2, '2025-01-12'), -- Bruno -> Mouse Gamer RGB
(2, 5, 1, '2025-02-03'), -- Bruno -> Monitor
(2, 8, 3, '2025-02-25'), -- Bruno -> Camiseta Naruto

(3, 2, 1, '2025-01-22'), -- Carla -> Notebook Ultra Slim
(3, 6, 1, '2025-02-11'), -- Carla -> Gamepad 54

(4, 9, 1, '2025-02-08'), -- Diego -> SSD
(4, 10, 1, '2025-03-01'), -- Diego -> Headset

(5, 4, 1, '2025-02-14'), -- Eduarda -> Teclado
(5, 3, 2, '2025-03-02'), -- Eduarda -> Mouse

(6, 1, 1, '2025-02-05'), -- Felipe -> Notebook Gamer Nitro
(6, 6, 2, '2025-02-18'), -- Felipe -> Gamepad 54

(7, 2, 1, '2025-01-30'), -- Gabriela -> Notebook Ultra Slim
(7, 9, 1, '2025-02-28'), -- Gabriela -> SSD

(8, 7, 1, '2025-02-07'); -- Henrique -> Camiseta Star Wars
```

## 🧠 Revisão Rápida: Relacionamento entre Tabelas

Em bancos de dados relacionais, as tabelas se conectam através de chaves:

* **Chave primária (PK)**: identifica unicamente cada registro.
* **Chave estrangeira (FK)**: aponta para a chave primária de outra tabela.

No nosso banco:

* `clientes.id` → PK da tabela `clientes`
* `produtos.id` → PK da tabela `produtos`
* `compras.cliente_id` → FK para `clientes.id`
* `compras.produto_id` → FK para `produtos.id`

---

## 🔗 Consultando Múltiplas Tabelas com `WHERE`

Podemos relacionar tabelas especificando a condição diretamente no `WHERE`.

### Estrutura geral

```sql
SELECT tabela1.coluna, tabela2.coluna
FROM tabela1, tabela2
WHERE tabela1.chave = tabela2.chave;
```

### Exemplo com nosso banco

```sql
SELECT c.nome AS cliente, p.nome AS produto
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND p.preco > 1000;
```

---

## 🔍 Tipos de Relacionamentos no Nosso Banco

### 1. Relacionamento 1:N (Um para Muitos)

Um cliente pode realizar várias compras.

```sql
SELECT c.nome, co.id, co.data_compra
FROM clientes c, compras co
WHERE c.id = co.cliente_id;
```

### 2. Relacionamento N:M (Muitos para Muitos)

Um cliente pode comprar vários produtos e um produto pode ser comprado por vários clientes.
A tabela `compras` é a tabela intermediária que faz essa ligação.

```sql
SELECT c.nome, p.nome, co.quantidade
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id;
```

---

## 🛠️ Técnicas Úteis

### 1. Aliases para Tabelas

Aliases deixam a consulta menor e mais legível:

```sql
SELECT c.nome, p.nome
FROM clientes AS c, compras AS co, produtos AS p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND c.cidade = 'São Paulo'
  AND p.preco > 500;
```

---

### 2. Filtros Adicionais

Podemos combinar filtros de diferentes tabelas:

```sql
SELECT c.nome, p.nome
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND c.idade > 30
  AND p.categoria = 'Games'
  AND p.preco < 1000;
```

---

### 3. Ordenação Combinada

Também podemos ordenar usando colunas de tabelas diferentes:

```sql
SELECT c.nome, p.nome, p.preco
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
ORDER BY c.nome ASC, p.preco DESC;
```

---

## ⚠️ Cuidados Importantes

### 1. Produto cartesiano

Se você esquecer a condição de ligação no `WHERE`, o banco combina **todas as linhas com todas as linhas**.

Exemplo:

* 8 clientes × 10 produtos = **80 combinações**
* Se ainda incluir compras no meio, imaginem o caos.

Exemplo errado:

```sql
SELECT c.nome, p.nome
FROM clientes c, produtos p;
```

Isso **não relaciona** cliente com produto comprado — só mistura tudo.

---

### 2. Clareza nas colunas

Quando mais de uma tabela possui colunas com o mesmo nome, prefixe:

```sql
c.nome
p.nome
co.id
```

Isso evita ambiguidade e deixa a consulta mais fácil de entender.

---

### 3. Use aliases com consistência

Se começou com `c`, `co` e `p`, continue com eles até o final da consulta.

---

## 💡 Dicas

Em SQL existem outros tipos de operadores além dos básicos como:   

- `>` (maior que), 
- `<` (menor que), 
- `>=` (maior ou igual a), 
- `<=` (menor ou igual a) 
- `=` (igual a)   
  
Podemos utilizar também:

- `BETWEEN` - Significa `ENTRE` em inglês. No sentido de um valor estar entre uma coisa e outra. Não no sentido de entrar 😅   

Exemplo: 

```SQL
SELECT * FROM compras WHERE data_compra BETWEEN '2021-01-01' AND '2024-12-31'
```   
    
Essa consulta pega tudo da tabela compras onde a data da compra está entre `01/01/2021` e `31/12/2024`.   
Essa mesma consulta poderia ser feita de outra forma: 

```SQL
SELECT * FROM compras WHERE data_compra >= '2021-01-01' AND data_compra <= '2024-12-31'
```

- `LIKE` - O operador `LIKE` é usado para fazer buscas por padrões em campos de texto.

#### Coringas do `LIKE`

* `%` → representa **zero, um ou vários caracteres**.
* `_` → representa **exatamente um caractere**.

#### Exemplos com `%`

```sql
SELECT nome FROM produtos
WHERE nome LIKE 'C%';
```

Retorna nomes que começam com `C`:

```
Celular
Computador
Câmera
```

```sql
SELECT nome FROM produtos
WHERE nome LIKE '%fone%';
```

Retorna nomes que contêm `fone` em qualquer posição:

```
Telefone
Microfone
Fone de Ouvido
```

Outros exemplos:

```sql
WHERE nome LIKE '%a';   -- termina com "a"
WHERE nome LIKE '%ar%'; -- contém "ar"
WHERE nome LIKE '%';    -- qualquer texto
```

#### Exemplos com `_`

```sql
WHERE nome LIKE '_a%';
```

O primeiro caractere pode ser qualquer um, o segundo deve ser `a`:

```
Maria
Carlos
```

```sql
WHERE nome LIKE 'C___';
```

Retorna textos com 4 caracteres que começam com `C`:

```
Casa
Copo
```

```sql
WHERE nome LIKE '__';
```

Retorna textos com exatamente 2 caracteres.

#### Resumo

| Padrão   | Significado                          |
| -------- | ------------------------------------ |
| `C%`     | Começa com `C`                       |
| `%fone%` | Contém `fone`                        |
| `%a`     | Termina com `a`                      |
| `_a%`    | Segundo caractere é `a`              |
| `C___`   | Começa com `C` e possui 4 caracteres |
| `__`     | Possui exatamente 2 caracteres       |


### 🚀 Exemplos Práticos com Nosso Banco

### 1. Clientes que compraram produtos acima de R$ 1000

```sql
SELECT c.nome AS cliente, p.nome AS produto, p.preco
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND p.preco > 1000;
```

---

### 2. Clientes de Porto Alegre que compraram "Notebook"

```sql
SELECT c.nome AS cliente, p.nome AS produto
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND c.cidade = 'Porto Alegre'
  AND p.nome LIKE '%Notebook%';
```

---

### 3. Clientes de São Paulo com produtos de Informática, ordenados por preço decrescente

```sql
SELECT c.nome AS cliente, p.nome AS produto, p.preco
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND c.cidade = 'São Paulo'
  AND p.categoria = 'Informática'
ORDER BY p.preco DESC;
```

---

## 🧪 Consultas Extras Úteis no PostgreSQL

Como agora estamos no PostgreSQL, dá para aproveitar algumas coisas legais.

### Filtrar por mês/ano usando datas

#### Exemplo: compras feitas em fevereiro de 2025

```sql
SELECT c.nome, p.nome, co.data_compra
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND co.data_compra BETWEEN '2025-02-01' AND '2025-02-28';
```

> [!TIP]
> Se quiser algo mais flexível `EXTRACT(MONTH FROM data_compra)` e `EXTRACT(YEAR FROM data_compra)`.

Exemplo:

```sql
SELECT c.nome, p.nome, co.data_compra
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND EXTRACT(MONTH FROM co.data_compra) = 2
  AND EXTRACT(YEAR FROM co.data_compra) = 2025;
```

---

# 🏋️ Exercícios

1. Liste o nome dos clientes e os produtos que eles compraram.
2. Mostre os clientes que compraram mais de 1 unidade de qualquer produto.
3. Liste os produtos da categoria **"Eletrônicos"** comprados por clientes de **Canoas**.
4. Mostre os clientes que compraram **"Gamepad 54"**.
5. Liste todos os clientes que já compraram **"Notebook"**.
6. Mostre os nomes dos clientes e os preços dos produtos comprados acima de **R$ 1500**.
7. Liste clientes de **Salvador** que compraram produtos da categoria **"Informática"**.
8. Mostre todos os produtos que a cliente **"Ana Fernandes"** já comprou.
9. Liste todos os clientes que compraram produtos cujo nome começa com **"Camiseta"**.
10. Mostre todos os clientes e produtos comprados em **fevereiro de 2025**.

---

# 💡 Desafio Extra

Monte uma consulta que mostre:

* nome do cliente
* nome do produto
* quantidade comprada
* preço do produto
* valor total da compra (`quantidade * preco`)

Ordene do maior valor total para o menor.
