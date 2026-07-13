# 👾 Retro Games Database Challenge

## Desafio Final – Banco de Dados

## 📖 Contexto

A empresa **RetroTech Solutions**, especializada no desenvolvimento de sistemas para eventos e competições de videogames, foi contratada para desenvolver um sistema capaz de gerenciar um campeonato de jogos retrô.

O cliente pretende utilizar esse sistema em diversos eventos futuros, registrando equipes, jogadores, jogos, partidas e pontuações, além de gerar relatórios para acompanhar o desempenho dos participantes durante o campeonato.

Antes do desenvolvimento completo do sistema, a empresa solicitou que sua equipe realizasse o **planejamento do banco de dados**, implementasse sua estrutura e efetuasse testes utilizando dados reais obtidos durante um campeonato realizado em sala de aula.

Sua missão será atuar como uma equipe de desenvolvedores responsável pelo projeto desse banco de dados.

---

# 🎯 Objetivos

Ao final da atividade, sua equipe deverá ser capaz de:

* Planejar corretamente um banco de dados relacional;
* Modelar as entidades e seus relacionamentos;
* Implementar o banco utilizando PostgreSQL;
* Inserir os dados obtidos durante o campeonato;
* Desenvolver consultas SQL capazes de responder às necessidades do cliente.

---

# 🎮 O Campeonato

Durante a aula será realizado um campeonato de jogos retrô.

Cada equipe representará uma organização participante do campeonato e disputará partidas dos jogos definidos pelo professor.

Os resultados obtidos durante essas partidas serão utilizados como base para alimentar o banco de dados desenvolvido por cada grupo.

Ou seja, ao final da competição, cada equipe possuirá um banco de dados contendo todas as informações reais do campeonato.

---

# 📋 Requisitos do Sistema

Após uma reunião com o cliente, foram definidos os seguintes requisitos mínimos.

O sistema deverá permitir cadastrar:

* equipes participantes;
* jogadores pertencentes às equipes;
* jogos disponíveis no campeonato;
* campeonatos realizados;
* partidas disputadas;
* participação dos jogadores em cada partida;
* pontuação obtida por cada participante.

O banco deverá ser flexível para suportar novos campeonatos e novos jogos futuramente, sem necessidade de alterar sua estrutura.

---

# 📐 Planejamento

Antes de iniciar a implementação, deverá ser elaborado um **Diagrama Entidade-Relacionamento (DER)**.

O diagrama deverá representar corretamente:

* entidades;
* atributos;
* chaves primárias;
* chaves estrangeiras;
* relacionamentos;
* cardinalidades.

Após a conclusão do DER, o banco deverá ser implementado em PostgreSQL.

---

# ⚠️ Regras de Modelagem

Durante a reunião com o cliente, foi informado que um campeonato poderá possuir partidas com diferentes quantidades de participantes.

Por esse motivo, **não será aceita uma modelagem contendo colunas como:**

* jogador1
* jogador2
* jogador3
* equipe1
* equipe2
* vencedor
* perdedor

Os participantes das partidas deverão ser representados por uma estrutura adequada ao modelo relacional, permitindo registrar qualquer quantidade de participantes em uma mesma partida.

Essa decisão facilitará futuras consultas e permitirá reutilizar o sistema em diversos tipos de campeonatos.

---

# 🧪 Testes do Sistema

Após a implementação do banco de dados, será realizado um campeonato em sala de aula.

Os dados produzidos durante as partidas deverão ser inseridos no banco como forma de validar o funcionamento do sistema.

---

# 🔍 Funcionalidades solicitadas pelo cliente

Após os testes, o cliente deseja verificar se o banco de dados é capaz de responder às seguintes perguntas.

### 1. Quais jogadores pertencem a cada equipe?

---

### 2. Quais partidas foram disputadas?

Exiba:

* jogo;
* data;
* rodada;
* participantes;
* pontuação obtida.

---

### 3. Qual foi a pontuação total de cada equipe?

---

### 4. Qual é o ranking das equipes?

---

### 5. Qual é o ranking dos jogadores?

---

### 6. Qual foi a maior pontuação registrada em cada jogo?

---

### 7. Qual é a média de pontos obtida por cada equipe?

---

### 8. Qual foi a menor e a maior pontuação obtida por cada equipe?

---

### 9. Quantas partidas foram disputadas em cada jogo?

---

### 10. Quantas partidas cada jogador disputou?

---

### 11. Quais jogadores participaram de mais de uma partida?

Utilize a cláusula `HAVING`.

---

### 12. Gere uma classificação final do campeonato contendo:

* jogador;
* equipe;
* partidas disputadas;
* pontuação total.

Ordene os resultados da maior para a menor pontuação.

---

# 📦 Entregáveis

Cada equipe deverá entregar:

* DER do banco de dados;
* Script SQL contendo a criação do banco e das tabelas;
* Script SQL com os registros utilizados durante os testes;
* Script SQL contendo todas as consultas solicitadas;
* Banco de dados funcionando corretamente.
