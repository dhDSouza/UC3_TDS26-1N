# 📚 Aula 7: JOINs (INNER JOIN, LEFT JOIN e RIGHT JOIN)

## 🎯 Objetivo da Aula

Aprender a utilizar os principais tipos de **JOINs** do PostgreSQL para relacionar tabelas de forma mais organizada, legível e profissional.

Ao final da aula, o aluno será capaz de:

* Compreender o que é um `JOIN`;
* Utilizar `INNER JOIN`;
* Utilizar `LEFT JOIN`;
* Utilizar `RIGHT JOIN`;
* Identificar quando utilizar cada tipo de junção;
* Comparar consultas utilizando `WHERE` e `JOIN`.

---

# 🛠️ Banco de Dados

**Utilizaremos exatamente o mesmo banco da aula anterior.**

---

# 🧠 O que é um JOIN?

Na aula anterior fizemos consultas envolvendo várias tabelas utilizando o `WHERE`.

Exemplo:

```sql
SELECT c.nome, p.nome
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
AND p.id = co.produto_id;
```

Essa forma funciona perfeitamente.

Porém, existe uma maneira mais moderna, organizada e recomendada de fazer esse relacionamento: utilizando **JOIN**.

A mesma consulta fica assim:

```sql
SELECT c.nome, p.nome
FROM clientes c
INNER JOIN compras co
ON c.id = co.cliente_id
INNER JOIN produtos p
ON p.id = co.produto_id;
```

Observe que agora:

* o relacionamento fica explícito;
* cada ligação possui seu próprio `ON`;
* a consulta fica mais fácil de ler.

---

# 🎯 Estrutura Geral

```sql
SELECT colunas
FROM tabela1
JOIN tabela2
ON tabela1.chave = tabela2.chave;
```

---

# 🔵 INNER JOIN

É o JOIN mais utilizado.

Ele retorna **somente os registros que possuem correspondência nas duas tabelas**.

## Visualmente

```
Clientes        Compras

      ◯────────◯

Apenas a interseção.
```

---

## Exemplo 1

Mostrar clientes e seus produtos.

```sql
SELECT
    c.nome AS cliente,
    p.nome AS produto
FROM clientes c
INNER JOIN compras co
ON c.id = co.cliente_id
INNER JOIN produtos p
ON p.id = co.produto_id;
```

Resultado:

| Cliente | Produto              |
| ------- | -------------------- |
| Ana     | Notebook Gamer Nitro |
| Ana     | Camiseta Star Wars   |
| Bruno   | Mouse Gamer RGB      |
| ...     | ...                  |

---

## Exemplo 2

Produtos acima de R$1000

```sql
SELECT
    c.nome,
    p.nome,
    p.preco
FROM clientes c
INNER JOIN compras co
ON c.id = co.cliente_id
INNER JOIN produtos p
ON p.id = co.produto_id
WHERE p.preco > 1000;
```

---

## Exemplo 3

Clientes de Canoas

```sql
SELECT
    c.nome,
    p.nome,
    p.preco
FROM clientes c
INNER JOIN compras co
ON c.id = co.cliente_id
INNER JOIN produtos p
ON p.id = co.produto_id
WHERE c.cidade = 'Canoas';
```

---

# 🟢 LEFT JOIN

O `LEFT JOIN` retorna:

* todos os registros da tabela da esquerda;
* apenas os registros correspondentes da tabela da direita.

Quando não existir correspondência, os campos da direita aparecem como **NULL**.

---

## Visualmente

```
Clientes        Compras

██████████◯

Tudo da esquerda +
o que existir da direita.
```

---

## Exemplo simples

```sql
SELECT
    c.nome,
    co.data_compra
FROM clientes c
LEFT JOIN compras co
ON c.id = co.cliente_id;
```

Todos os clientes aparecerão.

Caso algum cliente nunca tenha comprado nada, a data ficará:

```
NULL
```

---

## Simulando um cliente sem compras

```sql
INSERT INTO clientes (nome, idade, cidade)
VALUES ('João Pedro', 30, 'Novo Hamburgo');
```

Agora execute:

```sql
SELECT
    c.nome,
    co.data_compra
FROM clientes c
LEFT JOIN compras co
ON c.id = co.cliente_id;
```

Resultado:

| Cliente    | Data       |
| ---------- | ---------- |
| Ana        | 2025-01-10 |
| Bruno      | 2025-01-12 |
| João Pedro | NULL       |

---

## Encontrando clientes sem compras

Essa é uma das utilizações mais comuns do `LEFT JOIN`.

```sql
SELECT
    c.nome
FROM clientes c
LEFT JOIN compras co
ON c.id = co.cliente_id
WHERE co.id IS NULL;
```

Resultado:

```
João Pedro
```

---

# 🟡 RIGHT JOIN

É o contrário do LEFT JOIN.

Retorna:

* todos os registros da tabela da direita;
* somente os registros correspondentes da esquerda.

---

## Visualmente

```
Clientes        Compras

      ◯██████████
```

---

## Exemplo

```sql
SELECT
    c.nome,
    co.data_compra
FROM clientes c
RIGHT JOIN compras co
ON c.id = co.cliente_id;
```

Como todas as compras possuem um cliente, o resultado será igual ao `INNER JOIN`.

---

## Quando usar?

Na prática, quase sempre utilizamos `LEFT JOIN`.

O `RIGHT JOIN` existe, mas muitos desenvolvedores preferem inverter a ordem das tabelas e utilizar `LEFT JOIN`.

Exemplo:

Em vez de:

```sql
SELECT *
FROM clientes
RIGHT JOIN compras
ON clientes.id = compras.cliente_id;
```

Fazemos:

```sql
SELECT *
FROM compras
LEFT JOIN clientes
ON clientes.id = compras.cliente_id;
```

O resultado é o mesmo.

---

# 🔍 Comparando os JOINs

| JOIN       | Retorna                                        |
| ---------- | ---------------------------------------------- |
| INNER JOIN | Apenas registros que existem nas duas tabelas  |
| LEFT JOIN  | Todos da esquerda + correspondentes da direita |
| RIGHT JOIN | Todos da direita + correspondentes da esquerda |

---

# 🎨 Comparando com Diagramas

## INNER JOIN

```
Clientes     Compras

    ◯
```

---

## LEFT JOIN

```
██████◯
```

---

## RIGHT JOIN

```
◯██████
```

---

# 🔧 JOIN com três tabelas

É muito comum ligar mais de duas tabelas.

```sql
SELECT
    c.nome,
    p.nome,
    co.quantidade,
    p.preco
FROM clientes c
INNER JOIN compras co
ON c.id = co.cliente_id
INNER JOIN produtos p
ON p.id = co.produto_id;
```

---

# 💰 Calculando o valor total

```sql
SELECT
    c.nome,
    p.nome,
    co.quantidade,
    p.preco,
    co.quantidade * p.preco AS total
FROM clientes c
INNER JOIN compras co
ON c.id = co.cliente_id
INNER JOIN produtos p
ON p.id = co.produto_id;
```

---

# 📅 Compras realizadas em fevereiro

```sql
SELECT
    c.nome,
    p.nome,
    co.data_compra
FROM clientes c
INNER JOIN compras co
ON c.id = co.cliente_id
INNER JOIN produtos p
ON p.id = co.produto_id
WHERE EXTRACT(MONTH FROM co.data_compra) = 2
AND EXTRACT(YEAR FROM co.data_compra) = 2025;
```

---

# 🛠️ Boas Práticas

✅ Utilize aliases.

```sql
clientes c
compras co
produtos p
```

---

✅ Faça o relacionamento no `ON`.

```sql
INNER JOIN compras co
ON c.id = co.cliente_id
```

---

✅ Utilize o `WHERE` apenas para filtros.

```sql
WHERE p.preco > 1000
```

---

✅ Indente a consulta.

Uma consulta organizada é muito mais fácil de entender.

---

# ⚠️ Erros Comuns

## Esquecer o ON

Errado:

```sql
SELECT *
FROM clientes
INNER JOIN compras;
```

O PostgreSQL retornará erro, pois falta informar como as tabelas se relacionam.

---

## Relacionar colunas incorretas

Errado:

```sql
ON clientes.id = produtos.id
```

Essas tabelas não possuem relacionamento direto.

---

## Misturar JOIN com relacionamento no WHERE

Evite fazer:

```sql
FROM clientes c
INNER JOIN compras co
WHERE c.id = co.cliente_id;
```

O correto é:

```sql
FROM clientes c
INNER JOIN compras co
ON c.id = co.cliente_id;
```

---

# 🧪 Exercícios

1. Liste o nome dos clientes e os produtos comprados utilizando `INNER JOIN`.
2. Mostre os clientes e as datas das compras.
3. Liste apenas os produtos da categoria **Informática** comprados pelos clientes.
4. Mostre os clientes que compraram produtos acima de **R$ 500**.
5. Liste todos os clientes utilizando `LEFT JOIN`, mostrando suas compras (caso existam).
6. Cadastre um novo cliente sem compras e utilize `LEFT JOIN` para verificar o resultado.
7. Mostre apenas os clientes que ainda não realizaram compras.
8. Faça uma consulta utilizando `RIGHT JOIN` retornando todas as compras e seus respectivos clientes.
9. Liste cliente, produto, quantidade e preço utilizando `INNER JOIN`.
10. Liste todas as compras realizadas em fevereiro de 2025.

---

# 🚀 Desafio Extra

Monte uma consulta que exiba:

* Nome do cliente;
* Cidade;
* Nome do produto;
* Categoria;
* Quantidade comprada;
* Preço unitário;
* Valor total da compra (`quantidade × preço`);
* Data da compra.

Requisitos:

* Utilize apenas `INNER JOIN`;
* Ordene pelo **valor total da compra** em ordem decrescente;
* Em caso de empate, ordene pelo nome do cliente em ordem alfabética.
