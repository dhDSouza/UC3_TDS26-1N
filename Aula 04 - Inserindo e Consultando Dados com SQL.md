# 📘 Aula 4 – Inserindo e Consultando Dados com SQL

## 🎯 Objetivo da Aula

Aprender a inserir registros em tabelas e realizar consultas básicas utilizando SQL.

Ao final da aula, você será capaz de:

* Inserir dados em tabelas;
* Consultar registros;
* Selecionar colunas específicas;
* Utilizar apelidos (AS);
* Entender o resultado de uma consulta SQL.

---

# 🧠 Relembrando

Na aula anterior aprendemos a:

* Criar bancos de dados;
* Criar tabelas;
* Definir chaves primárias;
* Definir chaves estrangeiras.

Agora vamos começar a trabalhar com os dados armazenados nessas tabelas.

---

# 📦 Comando INSERT INTO

O comando INSERT é utilizado para adicionar registros em uma tabela.

Sintaxe:

```sql
INSERT INTO tabela (coluna1, coluna2)
VALUES (valor1, valor2);
```

---

# Exemplo

Tabela:

```sql
CREATE TABLE aluno (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(150)
);
```

Inserindo um aluno:

```sql
INSERT INTO aluno (nome, email)
VALUES ('João Silva', 'joao@email.com');
```

---

# Inserindo Vários Registros

Também podemos inserir vários registros de uma vez.

```sql
INSERT INTO aluno (nome, email)
VALUES
    ('Maria Souza', 'maria@email.com'),
    ('Pedro Santos', 'pedro@email.com'),
    ('Ana Costa', 'ana@email.com');
```

---

# Verificando os Dados

Para visualizar os registros utilizamos o comando:

```sql
SELECT * FROM aluno;
```

Resultado esperado:

| id | nome         | email                                     |
| -- | ------------ | ----------------------------------------- |
| 1  | João Silva   | [joao@email.com](mailto:joao@email.com)   |
| 2  | Maria Souza  | [maria@email.com](mailto:maria@email.com) |
| 3  | Pedro Santos | [pedro@email.com](mailto:pedro@email.com) |
| 4  | Ana Costa    | [ana@email.com](mailto:ana@email.com)     |

---

# 🔍 Comando SELECT

O SELECT é utilizado para consultar informações armazenadas no banco.

Sintaxe:

```sql
SELECT coluna
FROM tabela;
```

---

# Consultando Todas as Colunas

```sql
SELECT *
FROM aluno;
```

O caractere * significa:

"Todas as colunas"

---

# Consultando Apenas Algumas Colunas

```sql
SELECT nome, email
FROM aluno;
```

Resultado:

| nome        | email                                     |
| ----------- | ----------------------------------------- |
| João Silva  | [joao@email.com](mailto:joao@email.com)   |
| Maria Souza | [maria@email.com](mailto:maria@email.com) |

---

# Utilizando Alias (AS)

Alias significa apelido.

Podemos renomear colunas no resultado.

Exemplo:

```sql
SELECT
    nome AS aluno,
    email AS contato
FROM aluno;
```

Resultado:

| aluno      | contato                                 |
| ---------- | --------------------------------------- |
| João Silva | [joao@email.com](mailto:joao@email.com) |

---

# Exemplo com Turmas

Tabela:

```sql
CREATE TABLE turma (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50)
);
```

Inserindo registros:

```sql
INSERT INTO turma (nome)
VALUES
    ('TDS 2025'),
    ('TDS 2026'),
    ('TDS Noite');
```

Consultando:

```sql
SELECT *
FROM turma;
```

---

# Inserindo Dados com Chave Estrangeira

Tabela:

```sql
CREATE TABLE aluno (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100),
    turma_id INT,

    CONSTRAINT fk_aluno_turma
        FOREIGN KEY (turma_id)
        REFERENCES turma(id)
);
```

Inserindo:

```sql
INSERT INTO aluno (nome, turma_id)
VALUES
    ('Lucas', 1),
    ('Mariana', 1),
    ('Carlos', 2);
```

Observe que o valor informado em turma_id deve existir na tabela turma.

---

# Erro Comum

Tentar inserir uma chave estrangeira inexistente.

Exemplo:

```sql
INSERT INTO aluno (nome, turma_id)
VALUES ('João', 999);
```

Resultado:

```text
ERROR:
violates foreign key constraint
```

O PostgreSQL impede relacionamentos inválidos.

---

# Ordem Correta de Inserção

Quando existem relacionamentos:

1. Inserir na tabela pai.
2. Inserir na tabela filha.

Exemplo:

```text
TURMA
 ↓
ALUNO
```

Primeiro:

```sql
INSERT INTO turma...
```

Depois:

```sql
INSERT INTO aluno...
```

---

# Exemplo Completo

```sql
CREATE TABLE turma (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50)
);

CREATE TABLE aluno (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100),
    turma_id INT,

    CONSTRAINT fk_aluno_turma
        FOREIGN KEY (turma_id)
        REFERENCES turma(id)
);

INSERT INTO turma (nome)
VALUES
    ('TDS Manhã'),
    ('TDS Noite');

INSERT INTO aluno (nome, turma_id)
VALUES
    ('João', 1),
    ('Maria', 1),
    ('Pedro', 2);

SELECT * FROM turma;

SELECT * FROM aluno;
```

---

# ✏️ Exercício 1

Crie registros para a tabela professor.

Insira pelo menos:

* 5 professores

Depois execute:

```sql
SELECT * FROM professor;
```

---

# ✏️ Exercício 2

Crie registros para a tabela disciplina.

Insira pelo menos:

* 5 disciplinas

Depois execute:

```sql
SELECT nome
FROM disciplina;
```

---

# ✏️ Exercício 3

Crie registros para:

* Curso
* Turma
* Aluno

Insira pelo menos:

* 3 cursos
* 3 turmas
* 5 alunos

Realize consultas utilizando SELECT.

---

# 🏆 Desafio

Crie as tabelas:

* Cliente
* Pedido

Relacionamento:

```text
Cliente 1:N Pedido
```

Insira:

* 3 clientes
* 5 pedidos

Depois execute:

```sql
SELECT * FROM cliente;

SELECT * FROM pedido;
```

---

# 🎒 Tarefa para a Próxima Aula

Pesquise sobre os comandos:

```sql
WHERE
ORDER BY
LIMIT
```
