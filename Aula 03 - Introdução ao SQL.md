# 📘 Aula 3 – Introdução ao SQL com PostgreSQL e pgAdmin

## 🎯 Objetivo da Aula

Aprender a criar bancos de dados e tabelas utilizando SQL no PostgreSQL.

Ao final da aula, você será capaz de:

* Criar um banco de dados;
* Criar tabelas;
* Definir tipos de dados;
* Utilizar chave primária (PRIMARY KEY);
* Utilizar chave estrangeira (FOREIGN KEY);
* Executar comandos SQL utilizando o pgAdmin.

---

# 🧠 O que é SQL?

SQL significa:

**Structured Query Language**

É a linguagem utilizada para criar, consultar e manipular bancos de dados relacionais.

Com SQL podemos:

* Criar bancos de dados;
* Criar tabelas;
* Inserir dados;
* Consultar informações;
* Atualizar registros;
* Excluir registros.

---

# 🖥️ Conhecendo o pgAdmin

O pgAdmin é a ferramenta gráfica utilizada para administrar o PostgreSQL.

Principais áreas:

### Browser

Exibe:

* Servidores
* Bancos de Dados
* Schemas
* Tabelas

### Query Tool

Local onde escrevemos e executamos comandos SQL.

Para abrir:

Tools → Query Tool

---

# 🏗️ Criando um Banco de Dados

Sintaxe:

```sql
CREATE DATABASE escola;
```

Execute o comando no Query Tool.

Após criar o banco:

1. Atualize a lista de bancos.
2. Clique com o botão direito no banco.
3. Selecione Connect Database.

---

# 📦 Tipos de Dados Básicos

## Inteiros

```sql
INT
```

Exemplos:

* idade
* quantidade
* estoque

---

## Texto

```sql
VARCHAR(100)
```

Exemplos:

* nome
* email
* endereço

---

## Data

```sql
DATE
```

Exemplos:

* nascimento
* matrícula
* contratação

---

## Valores Monetários

```sql
DECIMAL(10,2)
```

Exemplos:

* preço
* salário
* valor_total

---

# 🔑 Chave Primária

A chave primária identifica um registro de forma única.

Exemplo:

```sql
id INT PRIMARY KEY
```

Nenhum registro poderá repetir esse valor.

---

# 🤖 Auto Incremento no PostgreSQL

No PostgreSQL utilizamos:

```sql
SERIAL
```

Exemplo:

```sql
id SERIAL PRIMARY KEY
```

O banco gera os IDs automaticamente.

---

# 🏗️ Criando a Primeira Tabela

Tabela de alunos:

```sql
CREATE TABLE aluno (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(150),
    data_nascimento DATE
);
```

Executando:

▶ Execute o comando.

Após executar:

Schemas → public → Tables

A tabela deverá aparecer.

---

# 🔍 Visualizando a Estrutura

Comando:

```sql
SELECT * FROM aluno;
```

Neste momento a tabela estará vazia.

Resultado esperado:

```text
0 linhas retornadas
```

---

# 🔗 Chave Estrangeira

Utilizamos chave estrangeira para criar relacionamentos entre tabelas.

Exemplo:

Um aluno pertence a uma turma.

---

# Criando a Tabela Turma

```sql
CREATE TABLE turma (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50) NOT NULL
);
```

---

# Criando a Relação

```sql
CREATE TABLE aluno (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(150),

    turma_id INT,

    CONSTRAINT fk_aluno_turma
        FOREIGN KEY (turma_id)
        REFERENCES turma(id)
);
```

---

# Entendendo o Relacionamento

```text
TURMA
  |
  | 1
  |
  | N
ALUNO
```

Uma turma possui vários alunos.

Cada aluno pertence a uma única turma.

---

# Exemplo Completo

```sql
CREATE TABLE turma (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50) NOT NULL
);

CREATE TABLE aluno (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(150),

    turma_id INT,

    CONSTRAINT fk_aluno_turma
        FOREIGN KEY (turma_id)
        REFERENCES turma(id)
);
```

---

# ✏️ Exercício 1

Crie uma tabela chamada professor.

Campos:

* id
* nome
* email
* especialidade

Utilize:

* SERIAL
* PRIMARY KEY
* VARCHAR

---

# ✏️ Exercício 2

Crie uma tabela chamada disciplina.

Campos:

* id
* nome
* carga_horaria

---

# ✏️ Exercício 3

Crie uma tabela chamada curso.

Campos:

* id
* nome
* descricao

---

# 🏆 Desafio

Crie o banco de dados de uma biblioteca contendo:

### Livro

* id
* titulo
* ano_publicacao

### Autor

* id
* nome
* nacionalidade

### Autoria

* id
* livro_id
* autor_id

Implemente todas as chaves estrangeiras.

---

# 🎒 Tarefa para Próxima Aula

Utilizando o DER criado na Aula 2:

1. Identifique as entidades.
2. Crie as tabelas correspondentes.
3. Defina a chave primária de cada tabela.
4. Crie as chaves estrangeiras necessárias.

Na próxima aula vamos aprender a inserir registros utilizando:

```sql
INSERT INTO
```

e realizar consultas utilizando:

```sql
SELECT
```
