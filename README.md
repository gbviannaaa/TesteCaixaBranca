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

### 1. **Problema de Conexão com o Banco de Dados**

**Erro**: Ao tentar executar o código, o banco de dados não estava sendo acessado corretamente. A mensagem de erro era:  
`Access denied for user 'root'@'localhost' (using password: YES)`

**Solução**: O problema foi corrigido ajustando a senha no código para corresponder à senha configurada no MySQL.

### 2. **Injeção de SQL**

**Erro**: A consulta SQL estava vulnerável a injeção de SQL, já que o `login` e a `senha` eram concatenados diretamente na query.

**Solução**: Para resolver esse problema, substituímos a concatenação direta por um `PreparedStatement`, que é uma forma segura de executar consultas SQL e evita vulnerabilidades de injeção.

### 3. **Erro de Conexão**

**Erro**: Mesmo após a correção da senha, o código ainda apresentava falhas na conexão com o banco devido à configuração incorreta da URL de conexão.

**Solução**: A URL foi ajustada para incluir o parâmetro `serverTimezone=UTC`, que é necessário para garantir a compatibilidade de horário entre o Java e o MySQL.

### 4. **Outros Ajustes**

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
