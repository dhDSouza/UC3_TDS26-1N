# 📘 Aula 2 – Modelagem Conceitual na Prática

## 🎯 Objetivo da Aula

Aprender a identificar entidades, atributos e relacionamentos a partir de situações reais e representar essas informações em um Diagrama ER (Entidade-Relacionamento).

Nesta aula, vamos focar principalmente na prática de modelagem, desenvolvendo a habilidade de transformar problemas do mundo real em modelos de banco de dados.

---

# 🧠 Conceitos Essenciais

## 📦 Entidade

Uma entidade é algo sobre o qual desejamos armazenar informações.

Exemplos:

* Aluno
* Produto
* Cliente
* Livro
* Professor

---

## 🏷️ Atributo

Um atributo é uma característica de uma entidade.

Exemplos:

### Aluno

* matrícula
* nome
* data_nascimento

### Produto

* código
* nome
* preço

---

## 🔗 Relacionamento

Representa a ligação entre entidades.

Exemplo:

* Um aluno realiza matrícula em uma turma.
* Um cliente realiza pedidos.
* Um médico atende pacientes.

---

## 🔢 Cardinalidades

As cardinalidades indicam quantas ocorrências de uma entidade podem se relacionar com outra.

### 1 : 1

`Uma` pessoa usa `um` computador.

### 1 : N

`Um` cliente pode realizar `vários` pedidos.

### N : N

`Um` aluno pode cursar `várias` disciplinas e `uma` disciplina pode possuir `vários` alunos.

---

# ✏️ Exemplo Resolvido

## Sistema de Cursos

### Entidades

**Aluno**

* id
* nome
* email

**Curso**

* id
* nome
* carga_horaria

### Relacionamento

`Um` aluno pode se matricular em `vários` cursos.

`Um` curso pode possuir `vários` alunos.

Cardinalidade:

**N : N**

---

# 🧩 Exercícios de Modelagem

Para cada situação abaixo:

1. Identifique as entidades.
2. Identifique os atributos.
3. Identifique os relacionamentos.
4. Identifique as cardinalidades.
5. Crie o Diagrama ER.

---

## Exercício 1 – Academia

Uma academia possui alunos e professores.

Regras:

* Cada professor pode orientar vários alunos.
* Cada aluno possui matrícula, nome e telefone.
* Cada professor possui nome e CREF.

---

## Exercício 2 – Clínica Médica

Uma clínica possui médicos e pacientes.

Regras:

* Um médico pode atender vários pacientes.
* Um paciente pode consultar vários médicos.
* Cada médico possui CRM e especialidade.
* Cada paciente possui CPF e data de nascimento.

---

## Exercício 3 – Biblioteca

Uma biblioteca controla livros e autores.

Regras:

* Um autor pode escrever vários livros.
* Um livro pode possuir vários autores.
* Cada livro possui título e ano de publicação.
* Cada autor possui nome e nacionalidade.

---

## Exercício 4 – Pizzaria

Uma pizzaria registra clientes e pedidos.

Regras:

* Um cliente pode realizar vários pedidos.
* Cada pedido possui data e valor total.
* Um pedido pode conter várias pizzas.
* Uma pizza pode aparecer em vários pedidos.
* Cada pizza possui nome e preço.

---

## Exercício 5 – Locadora de Filmes

Uma locadora registra clientes, filmes e locações.

Regras:

* Um cliente pode realizar várias locações.
* Cada locação possui data e valor.
* Uma locação pode conter vários filmes.
* Um filme pode estar presente em várias locações.
* Cada filme possui nome e categoria.

---

# 🏆 Desafio Final

Modele o sistema abaixo completo.

## Sistema Escolar

A escola possui:

* Alunos
* Professores
* Disciplinas
* Turmas

Regras:

* Um professor pode ministrar várias disciplinas.
* Uma disciplina pode ser ministrada por vários professores.
* Alunos podem estar matriculados em várias turmas.
* Cada turma possui vários alunos.
* Cada turma pertence a uma disciplina.

### Sua tarefa

1. Identificar todas as entidades.
2. Definir os atributos de cada entidade.
3. Identificar os relacionamentos.
4. Definir as cardinalidades.
5. Criar o Diagrama ER completo.

---

# 🎒 Tarefa para a Próxima Aula

Escolha um dos temas abaixo (ou outro tema simples de sua preferência):

* Escola
* Mercado
* Clínica
* Hotel
* Biblioteca
* Academia
* Pizzaria

Crie um Diagrama ER contendo:

* Pelo menos 3 entidades
* Pelo menos 2 relacionamentos
* Uso de cardinalidades
* Pelo menos um relacionamento 1:N ou N:N

> [!NOTE]
> Salve o diagrama e leve para a próxima aula. Vamos transformá-lo em um modelo lógico e começar a preparar o banco de dados para implementação.
