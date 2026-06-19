# 📘 Aula 5 – Atualizando e Removendo Dados com SQL

## 🎯 Objetivo da Aula

Aprender a modificar e remover registros em tabelas utilizando SQL, além de aprofundar consultas com filtros e ordenação.

Ao final da aula, você será capaz de:

* Atualizar dados existentes com **UPDATE**;
* Remover registros com **DELETE**;
* Filtrar consultas com **WHERE**;
* Ordenar resultados com **ORDER BY**;
* Limitar resultados com **LIMIT**;
* Entender o impacto dessas operações no banco de dados.

---

# 🧠 Relembrando

Na aula anterior aprendemos a:

* Inserir dados com **INSERT INTO**;
* Consultar dados com **SELECT**;
* Usar apelidos com **AS**;
* Trabalhar com chaves estrangeiras.

Agora vamos aprender a **alterar e remover dados já existentes**.

---

# ✏️ Atualizando Dados com UPDATE

O comando **UPDATE** é usado para modificar registros já existentes.

## Sintaxe:

```sql
UPDATE tabela
SET coluna = novo_valor
WHERE condição;
```

---

> [!IMPORTANT]
> Sempre use `WHERE`, senão todos os registros da tabela serão alterados!

<div align="center">
    <img src="https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExN2JuNXF1c2s4OG0ydGF2bGNtdnd5MXdpcm54azBlNzF5dHc2bjM2YSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xT4uQ7N8UNsoeFAjVS/giphy.gif" alt="Você está demitido">
    <p>
        Fonte: <em><a href="https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExN2JuNXF1c2s4OG0ydGF2bGNtdnd5MXdpcm54azBlNzF5dHc2bjM2YSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xT4uQ7N8UNsoeFAjVS/giphy.gif" target="_blank">https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExN2JuNXF1c2s4OG0ydGF2bGNtdnd5MXdpcm54azBlNzF5dHc2bjM2YSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xT4uQ7N8UNsoeFAjVS/giphy.gif</a></em>
    </p>
</div>  


---

## Exemplo básico

```sql
UPDATE aluno
SET email = 'novoemail@email.com'
WHERE id = 1;
```

---

## Exemplo com múltiplas colunas

```sql
UPDATE aluno
SET nome = 'João da Silva',
    email = 'joao.silva@email.com'
WHERE id = 1;
```

---

## Exemplo com chave estrangeira

```sql
UPDATE aluno
SET turma_id = 2
WHERE id = 3;
```

---

# 🗑️ Removendo Dados com DELETE

O comando **DELETE** remove registros de uma tabela.

## Sintaxe:

```sql
DELETE FROM tabela
WHERE condição;
```

---

## Exemplo básico

```sql
DELETE FROM aluno
WHERE id = 2;
```

---

## ⚠️ IMPORTANTE

Sem WHERE, todos os dados serão apagados:

```sql
DELETE FROM aluno;
```

🚨 Isso apaga todos os registros da tabela.

---

# 🔍 Filtrando Dados com WHERE

O **WHERE** permite selecionar registros específicos.

## Exemplo:

```sql
SELECT *
FROM aluno
WHERE turma_id = 1;
```

---

## Operadores comuns

| Operador | Significado    |
| -------- | -------------- |
| =        | Igual          |
| <>       | Diferente      |
| >        | Maior que      |
| <        | Menor que      |
| >=       | Maior ou igual |
| <=       | Menor ou igual |

---

## Exemplo com texto

```sql
SELECT *
FROM aluno
WHERE nome = 'João';
```

---

# 📊 Ordenando Resultados com ORDER BY

O **ORDER BY** organiza os dados.

## Sintaxe:

```sql
SELECT *
FROM tabela
ORDER BY coluna ASC;
```

---

## Ordem crescente (padrão)

```sql
SELECT *
FROM aluno
ORDER BY nome ASC;
```

---

## Ordem decrescente

```sql
SELECT *
FROM aluno
ORDER BY nome DESC;
```

---

# 🔢 Limitando Resultados com LIMIT

O **LIMIT** restringe a quantidade de resultados.

## Exemplo:

```sql
SELECT *
FROM aluno
LIMIT 3;
```

---

## Exemplo combinado

```sql
SELECT *
FROM aluno
ORDER BY nome ASC
LIMIT 2;
```

---

# 🔗 Combinando Tudo

Podemos usar vários comandos juntos:

```sql
SELECT nome, email
FROM aluno
WHERE turma_id = 1
ORDER BY nome ASC
LIMIT 5;
```

---

# 🧪 Exemplo Completo

```sql
-- Atualizar aluno
UPDATE aluno
SET nome = 'Maria Oliveira'
WHERE id = 2;

-- Remover aluno
DELETE FROM aluno
WHERE id = 3;

-- Consultar alunos da turma 1
SELECT *
FROM aluno
WHERE turma_id = 1
ORDER BY nome ASC;
```

---

# ⚠️ Erros Comuns

## 1. Esquecer o WHERE no UPDATE

```sql
UPDATE aluno
SET turma_id = 2;
```

> [!CAUTION]
> **Atualiza TODOS os registros.**

---

## 2. Esquecer o WHERE no DELETE

```sql
DELETE FROM aluno;
```

> [!CAUTION]
> **Apaga TODOS os dados da tabela.**

---

## 3. Usar LIMIT sem ORDER BY

```sql
SELECT *
FROM aluno
LIMIT 3;
```

> **Resultado pode variar a cada execução.**

---

# 🏆 Exercícios

## ✏️ Exercício 1 – UPDATE

Atualize:

* 2 alunos
* 1 turma

---

## ✏️ Exercício 2 – DELETE

Remova:

* 1 aluno específico
* 1 registro de disciplina (se existir)

---

## ✏️ Exercício 3 – SELECT com WHERE

Liste:

* Alunos da turma 1
* Alunos com id maior que 2

---

## ✏️ Exercício 4 – ORDER BY e LIMIT

* Liste alunos em ordem alfabética
* Mostre apenas os 3 primeiros registros

---

Perfeito — segue apenas a nova versão da seção **🏆 Desafio**, sem repetir o anterior:

---

# 🏆 Desafio

Utilizando uma tabela de **alunos**, crie situações práticas para treinar atualização, remoção e consultas:

1. Atualize o nome e o e-mail de 2 alunos diferentes.
2. Altere a turma de pelo menos 1 aluno.
3. Remova 1 aluno com base no ID.
4. Liste todos os alunos ordenados por nome em ordem decrescente.
5. Exiba apenas os 2 primeiros alunos cadastrados (ordenados por ID).
6. Liste todos os alunos que pertencem a uma turma específica.
