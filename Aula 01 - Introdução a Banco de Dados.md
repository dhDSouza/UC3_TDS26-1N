# 💾 **Aula 1: Introdução a Banco de Dados**

## 🧠 O que é um Banco de Dados?

Um **Banco de Dados** é como um **arquivo digital super organizado** onde armazenamos dados que podem ser facilmente acessados, manipulados e atualizados.

📦 **Analogia**: Imagine um **armário de arquivos** em um escritório. Cada gaveta representa uma **tabela**, cada pasta dentro da gaveta representa um **registro** (linha), e cada folha na pasta representa um **campo** (coluna). O Banco de Dados é esse armário digital.

---

## 🤔 Para que serve um Banco de Dados?

* Armazenar dados de forma estruturada
* Facilitar consultas e relatórios 📊
* Garantir segurança, integridade e consistência dos dados 🔒
* Trabalhar com grandes volumes de dados de forma eficiente
* Tornar sistemas dinâmicos (como apps e sites)

🖥️ Exemplos do dia a dia:

* Redes sociais (salvam seus posts, curtidas, comentários)
* E-commerces (produtos, preços, pedidos, estoque)
* Apps de transporte (corridas, rotas, usuários, motoristas)

---

## 📍 Dado X Informação

### 🔢 **Dado**

É um **fato bruto**, sem contexto. Exemplo:

* “123”
* “Marcos”
* “10/10/2000”

### 📚 **Informação**

É o dado **organizado** e com **contexto**. Exemplo:

* “123” → número do pedido de um cliente.
* “Marcos” → nome do cliente que fez o pedido.
* “10/10/2000” → data de nascimento do cliente.

📌 **Resumo**:

> **Dado** é a matéria-prima.
> **Informação** é o produto final.

---

## 🛠️ Tipos de Banco de Dados

### 📊 Relacional (SQL)

* Organizado em tabelas
* Usa linguagem SQL
* Ex: MySQL, PostgreSQL, SQL Server

### 📁 Não Relacional (NoSQL)

* Organizado por documentos, chave-valor, grafos, etc.
* Ex: MongoDB, Redis, Neo4j

---

## 🧱 Estrutura de um Banco de Dados Relacional

1. **Banco** → Conjunto de tabelas
2. **Tabela** → Estrutura de linhas (registros) e colunas (campos)
3. **Registro** → Linha com os dados de uma entidade
4. **Campo** → Coluna que define um tipo de dado

---

# 🔍 Modelagem de Dados: o primeiro passo antes do SQL

Antes de sair criando tabelas no banco, precisamos **planejar** como os dados estarão organizados. Isso se chama **Modelagem de Dados**.

---

## 🧠 Modelos de Banco de Dados

A modelagem é dividida em 3 níveis:

### 1️⃣ Modelo Conceitual (nível alto)

* Representado por **diagramas ER** (Entidade-Relacionamento)
* Mostra entidades, atributos e relacionamentos
* Ferramentas: BRModelo, Draw\.io, dbdiagram.io

📐 **Analogia**: planta baixa da casa. Serve pra entender a estrutura antes de construir.

---

### 2️⃣ Modelo Lógico

* Representa **como os dados serão organizados nas tabelas**
* Define as **chaves primárias**, **chaves estrangeiras**, tipos de relacionamento
* Já não tem atributos multivalorados ou compostos

📘 **Exemplo**:
Entidade `Cliente` com atributos → vira tabela `clientes` com colunas: `id`, `nome`, `cpf`, `data_nascimento`, etc.

---

### 3️⃣ Modelo Físico

* Representa **o banco de dados pronto pra rodar**, com detalhes técnicos
* Define os **tipos de dados reais** (`VARCHAR(100)`, `INT`, etc.)
* Compatível com o SGBD (MySQL, PostgreSQL, etc.)

🛠️ **Analogia**: a construção final da casa, com materiais reais.

---

## 🆚 Diferença entre Modelo Lógico e Físico

| Modelo | O que representa                                 | Nível de detalhe | Exemplo de dado                                                     |
|:------:|:------------------------------------------------:|:----------------:|:-------------------------------------------------------------------:|
| Lógico | Estrutura das tabelas e relacionamentos          | Médio            | `cliente (id, nome, cpf)`                                           |
| Físico | Estrutura com tipos reais e chaves implementadas | Alto             | `CREATE TABLE cliente (id INT, nome VARCHAR(100), cpf VARCHAR(11))` |

---

# 📚 Começando com o Modelo Lógico

### Como criar?

1. **Identifique as entidades** (ex: Cliente, Produto, Pedido)
2. **Defina os atributos** de cada entidade
3. **Escolha a chave primária** (PK - identificador único)
4. **Analise os relacionamentos** (1:1, 1\:N, N\:N)
5. **Crie as tabelas lógicas**

---

### 🧠 Exemplo:

Sistema de vendas simples:

* Entidades:

  * Cliente (id, nome, cpf)
  * Produto (id, nome, preco)
  * Pedido (id, data, cliente_id)

Relacionamentos:

* Um cliente pode fazer vários pedidos (1\:N)
* Um pedido pode ter vários produtos e um produto pode estar em vários pedidos (N\:N) → Tabela intermediária: `pedido_produto`

* Pedido_Produto (pedido_id, produto_id, quantidade)

---

## 🛠️ Ferramentas para Modelar

* [BRModelo](https://github.com/kevinrpb/brmodelo-web)
* [dbdiagram.io](https://dbdiagram.io)
* [Draw.io](https://app.diagrams.net)

---

# ✅ Exercícios

### 🧠 Teóricos

1. Explique com suas palavras a diferença entre **dado** e **informação**.
2. Para que serve um banco de dados?
3. Cite exemplos de onde encontramos bancos de dados no dia a dia.

### 🧩 Práticos

4. Crie um modelo lógico com as seguintes entidades:

   * **Aluno** (id, nome, data_nascimento)
   * **Curso** (id, nome, carga_horaria)
   * Um aluno pode se matricular em vários cursos (relacionamento N\:N)

5. Qual seria a chave primária e chave estrangeira no relacionamento acima?
