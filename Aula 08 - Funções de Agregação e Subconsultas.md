# 📚 Aula 8: Funções de Agregação e Subconsultas

## 🎯 Objetivo da Aula

Aprender a utilizar as principais **funções de agregação** do PostgreSQL para gerar estatísticas e relatórios, além de utilizar **subconsultas (Subqueries)** para resolver consultas mais avançadas.

Ao final da aula, o aluno será capaz de:

* Utilizar `COUNT()`;
* Utilizar `SUM()`;
* Utilizar `AVG()`;
* Utilizar `MIN()` e `MAX()`;
* Utilizar `GROUP BY`;
* Utilizar `HAVING`;
* Criar subconsultas;
* Utilizar subconsultas com `IN`, `EXISTS` e comparações;
* Resolver consultas mais complexas utilizando os conceitos aprendidos.

---

# 🛠️ Banco de Dados

Utilizaremos exatamente o mesmo banco de dados da aula anterior.

---

# 🧠 O que são Funções de Agregação?

As funções de agregação servem para realizar cálculos sobre um conjunto de registros.

Ao invés de retornar uma linha para cada registro, elas retornam um resultado resumido.

Exemplos:

* Quantidade de clientes
* Média de preços
* Produto mais caro
* Valor total vendido
* Total de compras

---

# 📌 Principais Funções

| Função    | Descrição       |
| --------- | --------------- |
| `COUNT()` | Conta registros |
| `SUM()`   | Soma valores    |
| `AVG()`   | Calcula média   |
| `MIN()`   | Menor valor     |
| `MAX()`   | Maior valor     |

---

# 🔢 COUNT()

Conta registros.

## Exemplo 1

Quantos clientes existem?

```sql
SELECT COUNT(*) AS total_clientes
FROM clientes;
```

Resultado

| total_clientes |
| -------------: |
|              8 |

---

## Exemplo 2

Quantos produtos existem?

```sql
SELECT COUNT(*) AS total_produtos
FROM produtos;
```

---

## Exemplo 3

Quantas compras foram realizadas?

```sql
SELECT COUNT(*) AS total_compras
FROM compras;
```

---

# ➕ SUM()

Soma valores.

## Exemplo 1

Quantidade total de produtos vendidos.

```sql
SELECT SUM(quantidade) AS total_itens
FROM compras;
```

---

## Exemplo 2

Valor total movimentado pela loja.

```sql
SELECT
    SUM(co.quantidade * p.preco) AS faturamento
FROM compras co
INNER JOIN produtos p
ON p.id = co.produto_id;
```

---

# 📊 AVG()

Calcula médias.

## Exemplo

Preço médio dos produtos.

```sql
SELECT AVG(preco) AS preco_medio
FROM produtos;
```

---

Também podemos arredondar:

```sql
SELECT ROUND(AVG(preco), 2) AS preco_medio
FROM produtos;
```

---

# 📈 MIN() e MAX()

## Produto mais barato

```sql
SELECT MIN(preco)
FROM produtos;
```

---

## Produto mais caro

```sql
SELECT MAX(preco)
FROM produtos;
```

---

## Cliente mais jovem

```sql
SELECT MIN(idade)
FROM clientes;
```

---

## Cliente mais velho

```sql
SELECT MAX(idade)
FROM clientes;
```

---

# 🧩 GROUP BY

Até agora os resultados eram gerais.

O `GROUP BY` permite dividir os registros em grupos.

Cada grupo terá sua própria agregação.

---

## Exemplo 1

Quantidade de clientes por cidade.

```sql
SELECT
    cidade,
    COUNT(*) AS total
FROM clientes
GROUP BY cidade;
```

Resultado

| Cidade       | Total |
| ------------ | ----: |
| Canoas       |     2 |
| Porto Alegre |     2 |
| Salvador     |     2 |
| São Paulo    |     2 |

---

## Exemplo 2

Quantidade de produtos por categoria.

```sql
SELECT
    categoria,
    COUNT(*) AS quantidade
FROM produtos
GROUP BY categoria;
```

---

## Exemplo 3

Preço médio por categoria.

```sql
SELECT
    categoria,
    ROUND(AVG(preco),2) AS media
FROM produtos
GROUP BY categoria;
```

---

## Exemplo 4

Total vendido por cliente.

```sql
SELECT
    c.nome,
    SUM(co.quantidade * p.preco) AS total_gasto
FROM clientes c
INNER JOIN compras co
ON c.id = co.cliente_id
INNER JOIN produtos p
ON p.id = co.produto_id
GROUP BY c.nome;
```

---

# 🎯 HAVING

O `WHERE` filtra registros.

O `HAVING` filtra grupos.

---

## Exemplo

Mostrar apenas clientes que gastaram mais de R$1000.

```sql
SELECT
    c.nome,
    SUM(co.quantidade * p.preco) AS total
FROM clientes c
INNER JOIN compras co
ON c.id = co.cliente_id
INNER JOIN produtos p
ON p.id = co.produto_id
GROUP BY c.nome
HAVING SUM(co.quantidade * p.preco) > 1000;
```

---

Outro exemplo:

Mostrar categorias que possuem mais de dois produtos.

```sql
SELECT
    categoria,
    COUNT(*) AS quantidade
FROM produtos
GROUP BY categoria
HAVING COUNT(*) > 2;
```

---

# 🧠 O que é uma Subconsulta?

Uma subconsulta (Subquery) é uma consulta dentro de outra consulta.

Ela é executada primeiro e seu resultado é utilizado pela consulta principal.

Estrutura:

```sql
SELECT ...
FROM tabela
WHERE coluna = (
    SELECT ...
);
```

---

# 📍 Subconsulta Escalar

Retorna apenas um valor.

## Exemplo

Mostrar o produto mais caro.

```sql
SELECT *
FROM produtos
WHERE preco = (
    SELECT MAX(preco)
    FROM produtos
);
```

---

Outro exemplo:

Mostrar o cliente mais velho.

```sql
SELECT *
FROM clientes
WHERE idade = (
    SELECT MAX(idade)
    FROM clientes
);
```

---

# 📍 Subconsulta com IN

Quando a subconsulta retorna vários registros.

## Exemplo

Mostrar todos os produtos da categoria Informática.

```sql
SELECT *
FROM produtos
WHERE categoria IN (
    SELECT categoria
    FROM produtos
    WHERE categoria = 'Informática'
);
```

Embora este exemplo seja simples, ele ilustra o funcionamento do `IN`.

---

Exemplo mais interessante:

Clientes que compraram notebooks.

```sql
SELECT *
FROM clientes
WHERE id IN (
    SELECT cliente_id
    FROM compras
    WHERE produto_id IN (
        SELECT id
        FROM produtos
        WHERE nome LIKE 'Notebook%'
    )
);
```

---

# 📍 Subconsulta com EXISTS

O `EXISTS` verifica se existe pelo menos um registro.

Ele retorna verdadeiro ou falso.

---

Clientes que realizaram compras.

```sql
SELECT *
FROM clientes c
WHERE EXISTS (
    SELECT 1
    FROM compras co
    WHERE co.cliente_id = c.id
);
```

---

Clientes sem compras.

```sql
SELECT *
FROM clientes c
WHERE NOT EXISTS (
    SELECT 1
    FROM compras co
    WHERE co.cliente_id = c.id
);
```

---

# 📍 Subconsulta na cláusula FROM

Também podemos utilizar uma consulta como uma tabela temporária.

Exemplo:

```sql
SELECT
    categoria,
    media
FROM (
    SELECT
        categoria,
        ROUND(AVG(preco),2) AS media
    FROM produtos
    GROUP BY categoria
) AS medias
WHERE media > 500;
```

---

# 🔄 Comparando JOIN e Subconsulta

Encontrar clientes que realizaram compras.

## Utilizando JOIN

```sql
SELECT DISTINCT c.nome
FROM clientes c
INNER JOIN compras co
ON c.id = co.cliente_id;
```

---

## Utilizando Subconsulta

```sql
SELECT nome
FROM clientes
WHERE id IN (
    SELECT cliente_id
    FROM compras
);
```

Ambas resolvem o problema.

A escolha depende da situação e da legibilidade da consulta.

---

# 💰 Relatório Completo

Quanto cada cliente gastou.

```sql
SELECT
    c.nome,
    COUNT(co.id) AS compras,
    SUM(co.quantidade) AS itens,
    SUM(co.quantidade * p.preco) AS total
FROM clientes c
INNER JOIN compras co
ON c.id = co.cliente_id
INNER JOIN produtos p
ON p.id = co.produto_id
GROUP BY c.nome
ORDER BY total DESC;
```

---

# 🛠️ Boas Práticas

✅ Utilize `GROUP BY` sempre que misturar agregações com outras colunas.

---

✅ Utilize `HAVING` apenas para filtros sobre agregações.

---

✅ Prefira `JOIN` quando precisar retornar dados de várias tabelas.

---

✅ Utilize subconsultas quando a lógica ficar mais clara ou quando um resultado depender de outro.

---

✅ Dê nomes (`AS`) para colunas calculadas.

---

# ⚠️ Erros Comuns

## Esquecer o GROUP BY

Errado:

```sql
SELECT
    nome,
    COUNT(*)
FROM clientes;
```

O PostgreSQL retornará erro, pois `nome` não está em uma função de agregação nem no `GROUP BY`.

---

## Utilizar WHERE com agregações

Errado:

```sql
SELECT cidade, COUNT(*)
FROM clientes
WHERE COUNT(*) > 1
GROUP BY cidade;
```

O correto é:

```sql
SELECT cidade, COUNT(*)
FROM clientes
GROUP BY cidade
HAVING COUNT(*) > 1;
```

---

## Subconsulta retornando vários valores

Errado:

```sql
SELECT *
FROM produtos
WHERE preco = (
    SELECT preco
    FROM produtos
);
```

A subconsulta retorna vários preços, causando erro.

Se forem esperados vários valores, utilize `IN`.

---

# 🧪 Exercícios

1. Conte quantos clientes existem cadastrados.
2. Conte quantos produtos existem na categoria **Eletrônicos**.
3. Calcule o preço médio de todos os produtos.
4. Mostre o produto mais caro e o mais barato.
5. Liste a quantidade de clientes por cidade.
6. Liste o preço médio dos produtos por categoria.
7. Mostre quanto cada cliente gastou no total.
8. Liste apenas os clientes que gastaram mais de **R$ 3.000**.
9. Encontre o(s) produto(s) com o maior preço utilizando uma subconsulta.
10. Liste os clientes que compraram algum produto da categoria **Informática** utilizando uma subconsulta.
11. Mostre os clientes que nunca realizaram compras utilizando `NOT EXISTS`.
12. Exiba as categorias cujo preço médio dos produtos seja superior a **R$ 500**.

---

# 🚀 Desafio Extra

Monte uma consulta que exiba:

* Nome do cliente;
* Cidade;
* Quantidade de compras realizadas;
* Quantidade total de itens comprados;
* Valor total gasto;
* Valor médio gasto por compra;
* Produto mais caro comprado pelo cliente.

### Requisitos

* Utilize `INNER JOIN`;
* Utilize pelo menos **três funções de agregação**;
* Utilize `GROUP BY`;
* Utilize `HAVING` para mostrar apenas clientes que gastaram mais de **R$ 2.000**;
* Utilize uma **subconsulta** para encontrar o produto mais caro comprado por cada cliente;
* Ordene pelo valor total gasto em ordem decrescente.
