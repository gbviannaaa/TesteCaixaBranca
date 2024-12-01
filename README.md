# Teste de Caixa Branca - Conexão com Banco de Dados MySQL

Este repositório contém o código para um projeto simples que realiza a autenticação de usuários em um banco de dados MySQL. O objetivo é verificar as credenciais de login e senha de um usuário e retornar o nome do usuário autenticado.

## Tecnologias Utilizadas

- **Java**: Linguagem principal utilizada no desenvolvimento.
- **MySQL**: Sistema de gerenciamento de banco de dados relacional utilizado para armazenar as credenciais de login dos usuários.

## Descrição do Projeto

O projeto é composto por duas classes principais:

- **`TesteCaixaBranca`**: Classe responsável por testar a autenticação do usuário.
- **`User`**: Classe que gerencia a conexão com o banco de dados, executa as consultas e retorna as informações do usuário.

A conexão é realizada com o banco de dados MySQL, e a autenticação ocorre verificando se o `login` e a `senha` correspondem a um usuário registrado na tabela `usuarios`.

## Erros Encontrados e Correções

Durante o desenvolvimento, foram identificados e corrigidos alguns problemas que comprometeriam o funcionamento do sistema:

### 1. Problema de Conexão com o Banco de Dados

**Erro**: Ao tentar executar o código, o banco de dados não estava sendo acessado corretamente. A mensagem de erro era:  
`Access denied for user 'root'@'localhost' (using password: YES)`

**Solução**: O problema foi corrigido ajustando a senha no código para corresponder à senha configurada no MySQL.

### 2. Injeção de SQL

**Erro**: A consulta SQL estava vulnerável a injeção de SQL, já que o `login` e a `senha` eram concatenados diretamente na query.

**Solução**: Para resolver esse problema, substituímos a concatenação direta por um `PreparedStatement`, que é uma forma segura de executar consultas SQL e evita vulnerabilidades de injeção.

### 3. Erro de Conexão

**Erro**: Mesmo após a correção da senha, o código ainda apresentava falhas na conexão com o banco devido à configuração incorreta da URL de conexão.

**Solução**: A URL foi ajustada para incluir o parâmetro `serverTimezone=UTC`, que é necessário para garantir a compatibilidade de horário entre o Java e o MySQL.

### 4. Outros Ajustes

Além dos problemas mais críticos, também foram feitas algumas melhorias gerais no código, como:

- Ajustes nas importações de bibliotecas.
- Correção da criação da instância do `Statement`.

## Estrutura do Banco de Dados

O banco de dados utilizado neste projeto é o MySQL e possui uma tabela chamada `usuarios`, com os seguintes campos:

```sql
CREATE DATABASE test;
USE test;

CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL,
    login VARCHAR(50) NOT NULL UNIQUE,
    senha VARCHAR(50) NOT NULL
);

INSERT INTO usuarios (nome, login, senha) VALUES
('João Silva', 'joao', '1234'),
('Maria Oliveira', 'maria', 'abcd');
```

## Etapa 3 - Caixa Branca: Análise de Fluxo, Complexidade Ciclomática e Caminhos

Nesta etapa, realizamos a análise de caixa branca do código do projeto. As atividades incluem a criação do grafo de fluxo, o cálculo da complexidade ciclomática e a identificação da base de caminhos.

### 1. Criação da Branch

- A branch **ETAPA 3** foi criada para realizar as alterações relacionadas a esta etapa do projeto.
- Nome da branch: `ETAPA 3`.

### 2. Grafo de Fluxo

#### 2.1. Identificação dos Nodos

O código foi analisado e os pontos de entrada e saída de valores foram identificados. Cada ponto relevante do código foi numerado para facilitar a construção do grafo de fluxo.

#### 2.2. Conexão entre Nodos (Arestas)

- O grafo de fluxo representa visualmente a sequência de execuções possíveis dentro do código, mostrando o caminho do controle a partir dos pontos de entrada até os pontos de saída.

**Grafo de Fluxo**:
```
   +-------+
   | Início|
   +-------+
       |
       v
   +------------+
   | Cria User  |
   +------------+
       |
       v
   +------------------+
   | Verifica usuário |
   +------------------+
       |
       v
   +---------------------+
   | Conecta ao banco    |
   +---------------------+
       |
       v
   +----------------------+
   | Executa consulta SQL |
   +----------------------+
       |
       v
   +---------------------+
   | Usuário autenticado?|
   +---------------------+
        /     \
   Sim /       \ Não
     /          \
    v            v
+---------+   +---------------+
| Sucesso |   | Falha         |
+---------+   +---------------+
     |
     v
   +--------+
   |  Fim   |
   +--------+

```

### 3. Complexidade Ciclomática

A complexidade ciclomática foi calculada com a fórmula:

\[
V(G) = E - N + 2P
\]

- **E**: Número de arestas no grafo de fluxo.
- **N**: Número de nodos no grafo de fluxo.
- **P**: Número de componentes conectados (geralmente 1 para programas simples).

**Resultado da complexidade ciclomática**: **3**

### 4. Base de Caminhos

A base de caminhos consiste nos caminhos independentes que podem ser seguidos no código, a partir dos pontos de entrada até os pontos de saída. Cada caminho é uma sequência única de instruções.

#### 4.1. Caminhos Identificados

1. **Caminho 1**: Fluxo sem erros — Conexão com o banco, execução da consulta e autenticação com sucesso.
2. **Caminho 2**: Erro de conexão ao banco — Falha na conexão ao banco de dados e exibição da mensagem de erro.
3. **Caminho 3**: Erro na consulta SQL — Falha na execução da consulta e exibição da falha na autenticação.

# Teste de Caixa Branca - Conexão com Banco de Dados MySQL

Este repositório contém o código de um projeto em Java que realiza a autenticação de usuários em um banco de dados MySQL. O objetivo é verificar as credenciais de login e senha de um usuário e retornar o nome do usuário autenticado.

## Tecnologias Utilizadas

- **Java**: Linguagem principal utilizada no desenvolvimento.
- **MySQL**: Sistema de gerenciamento de banco de dados relacional utilizado para armazenar as credenciais de login dos usuários.

## Descrição do Projeto

O projeto é composto por duas classes principais:

- **`TesteCaixaBranca`**: Classe responsável por testar a autenticação do usuário.
- **`User`**: Classe que gerencia a conexão com o banco de dados, executa as consultas e retorna as informações do usuário.

A conexão é realizada com o banco de dados MySQL, e a autenticação ocorre verificando se o `login` e a `senha` correspondem a um usuário registrado na tabela `usuarios`.

## Como Rodar o Projeto

1. Clone o repositório:
   ```bash
   git clone <url-do-repositorio>

