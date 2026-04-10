# Grupos de Comandos SQL

## Introdução

SQL (Structured Query Language) é a linguagem padrão para gerenciar bancos de dados relacionais. Os comandos SQL são organizados em quatro grupos principais, cada um com uma função específica no gerenciamento e manipulação de dados. Compreender esses grupos é fundamental para trabalhar eficientemente com bancos de dados.

---

## 1. DDL (Data Definition Language)

### O que é?

DDL ou **Linguagem de Definição de Dados** é responsável pela estrutura e esquema do banco de dados. Inclui comandos para criar, modificar e excluir objetos do banco de dados.

### Principais Comandos

| Comando | Descrição |
|---------|-----------|
| **CREATE** | Cria novos objetos no banco (tabelas, índices, views, etc.) |
| **ALTER** | Modifica a estrutura de objetos existentes |
| **DROP** | Remove objetos do banco de dados |
| **TRUNCATE** | Remove todos os registros de uma tabela (sem registrar a operação) |
| **RENAME** | Renomeia objetos do banco de dados |

### Exemplos

```sql
-- Criar uma tabela
CREATE TABLE usuarios (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    data_criacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Alterar uma tabela (adicionar coluna)
ALTER TABLE usuarios ADD COLUMN telefone VARCHAR(20);

-- Remover uma tabela
DROP TABLE usuarios;

-- Limpar todos os dados da tabela
TRUNCATE TABLE usuarios;
```

### Importância do DDL

- ✅ Define a **estrutura e organização** dos dados
- ✅ Garante **integridade referencial** através de constraints
- ✅ Melhora **performance** com índices e otimizações
- ✅ Organiza os dados de forma **lógica e eficiente**
- ✅ Essencial para o **design do banco de dados**

---

## 2. DML (Data Manipulation Language)

### O que é?

DML ou **Linguagem de Manipulação de Dados** é responsável pela manipulação dos dados dentro das tabelas. Inclui operações de inserção, atualização, exclusão e leitura de dados.

### Principais Comandos

| Comando | Descrição |
|---------|-----------|
| **INSERT** | Insere novos registros em uma tabela |
| **UPDATE** | Modifica dados existentes em uma tabela |
| **DELETE** | Remove registros de uma tabela |
| **SELECT** | Recupera dados de uma ou mais tabelas |

### Exemplos

```sql
-- Inserir um novo registro
INSERT INTO usuarios (nome, email, telefone) 
VALUES ('João Silva', 'joao@email.com', '119999999');

-- Inserir múltiplos registros
INSERT INTO usuarios (nome, email) VALUES 
('Maria Santos', 'maria@email.com'),
('Pedro Costa', 'pedro@email.com');

-- Atualizar dados
UPDATE usuarios 
SET email = 'joao.silva@email.com' 
WHERE id = 1;

-- Deletar registros
DELETE FROM usuarios 
WHERE id = 2;

-- Selecionar dados
SELECT * FROM usuarios WHERE nome LIKE '%Silva%';
```

### Importância do DML

- ✅ Permite **inserir, modificar e remover** dados
- ✅ Essencial para o **ciclo de vida dos dados**
- ✅ Realiza operações **CRUD** (Create, Read, Update, Delete)
- ✅ Mais utilizado no **dia a dia** do desenvolvimento
- ✅ Crítico para a **manutenção de dados** atualizados

---

## 3. DCL (Data Control Language)

### O que é?

DCL ou **Linguagem de Controle de Dados** é responsável pelo controle de acesso e permissões no banco de dados. Garante que apenas usuários autorizados possam acessar determinados dados.

### Principais Comandos

| Comando | Descrição |
|---------|-----------|
| **GRANT** | Concede permissões a um usuário ou grupo |
| **REVOKE** | Remove permissões previamente concedidas |
| **COMMIT** | Confirma as transações (salva mudanças permanentemente) |
| **ROLLBACK** | Desfaz as transações (reverte mudanças) |

### Exemplos

```sql
-- Conceder permissões ao usuário 'analista'
GRANT SELECT, INSERT, UPDATE ON banco_dados.* TO 'analista'@'localhost';

-- Conceder permissões específicas em uma tabela
GRANT SELECT ON usuarios TO 'leitor'@'localhost';

-- Revogar permissões
REVOKE UPDATE ON usuarios FROM 'analista'@'localhost';

-- Confirmar uma transação
COMMIT;

-- Desfazer uma transação
ROLLBACK;

-- Visualizar permissões de um usuário
SHOW GRANTS FOR 'analista'@'localhost';
```

### Importância do DCL

- ✅ Protege dados **sensíveis e confidenciais**
- ✅ Define **níveis de acesso** para diferentes usuários
- ✅ Garante **segurança** do banco de dados
- ✅ Implementa **controle de concorrência** com COMMIT/ROLLBACK
- ✅ Fundamental para **conformidade** com políticas de segurança

---

## 4. DQL (Data Query Language)

### O que é?

DQL ou **Linguagem de Consulta de Dados** é responsável pela recuperação de dados do banco de dados. Embora alguns a considerem parte do DML, é frequentemente tratada como um grupo separado pela sua importância e frequência de uso.

### Principais Comandos

| Comando | Descrição |
|---------|-----------|
| **SELECT** | Recupera dados de uma ou mais tabelas |
| **JOIN** | Combina dados de múltiplas tabelas |
| **WHERE** | Filtra resultados com condições |
| **GROUP BY** | Agrupa resultados por coluna |
| **ORDER BY** | Ordena os resultados |
| **HAVING** | Filtra grupos (usado com GROUP BY) |

### Exemplos

```sql
-- Consulta simples
SELECT id, nome, email FROM usuarios;

-- Com filtros (WHERE)
SELECT * FROM usuarios WHERE data_criacao > '2025-01-01';

-- Com junções (JOIN)
SELECT u.nome, p.titulo 
FROM usuarios u
INNER JOIN posts p ON u.id = p.usuario_id;

-- Com agregações
SELECT COUNT(*) as total, email 
FROM usuarios 
GROUP BY email 
HAVING COUNT(*) > 1;

-- Ordenar resultados
SELECT * FROM usuarios 
ORDER BY nome ASC 
LIMIT 10;
```

### Importância do DQL

- ✅ Permite **recuperar e analisar** dados
- ✅ Base para **relatórios e dashboards**
- ✅ Essencial para **business intelligence**
- ✅ Possibilita **filtragem e agregação** de dados
- ✅ Mais utilizado em **consultas diárias**

---

## Tabela Comparativa

| Aspecto | DDL | DML | DCL | DQL |
|--------|-----|-----|-----|-----|
| **Objetivo** | Estrutura do BD | Dados | Permissões | Consultas |
| **Reversível** | Não (cuidado!) | Sim | Sim | Não se aplica |
| **Exemplos** | CREATE, DROP | INSERT, UPDATE | GRANT, REVOKE | SELECT |
| **Frequência** | Ocasional | Frequente | Ocasional | Muito Frequente |
| **Risco** | Alto | Médio | Alto | Baixo |
| **Impacto** | Estrutural | Dados | Segurança | Leitura |

---

## Resumo e Conclusão

Os quatro grupos de comandos SQL trabalham juntos para fornecer um sistema completo de gerenciamento de banco de dados:

1. **DDL** → Define a estrutura do banco
2. **DML** → Manipula os dados
3. **DCL** → Controla o acesso aos dados
4. **DQL** → Consulta os dados

Dominar esses grupos é fundamental para qualquer profissional que trabalhe com bancos de dados, permitindo criar estruturas robustas, manter dados seguros e extrair informações valiosas para negócios.

---

**Última atualização:** 10 de abril de 2026
