# Implementação de Banco de Dados
---
## Aula 4
- **JOINS: https://github.com/Herysson/Implementacao-de-Banco-de-Dados/blob/main/Aula%2003%20-%20Consultas%20Joins.pdf**
<img width="592" height="458" alt="image" src="https://github.com/user-attachments/assets/05c06e30-756d-4dcf-9da0-118ef89903dc" />

```
-- Inner join
SELECT F.Pnome AS Nome, F.Unome AS Sobrenome, F.Endereco, D.Dnome AS Departamento
FROM FUNCIONARIO AS F
INNER JOIN DEPARTAMENTO AS D
ON F.Dnr = D.Dnumero
WHERE D.Dnome = 'Pesquisa';

SELECT F.Pnome AS Nome, F.Unome AS Sobrenome, F.Endereco, P.Projnome AS Projeto, T.Horas
FROM TRABALHA_EM AS T
INNER JOIN PROJETO AS P
ON T.Pnr = P.Projnumero
    INNER JOIN FUNCIONARIO AS F
    ON F.Cpf = T.Fcpf
WHERE P.Projnome = 'ProdutoX';

SELECT D.Dnome, P.Projnome, P.Projlocal, D.Cpf_gerente, F.Pnome, F.Unome, F.Endereco
FROM DEPARTAMENTO AS D
JOIN PROJETO AS P
ON P.Dnum = D.Dnumero
    JOIN FUNCIONARIO AS F
    ON F.Cpf = D.Cpf_gerente
WHERE P.Projlocal = 'Mauá'

-- Left join
SELECT F.Unome, D.Dnome
FROM FUNCIONARIO AS F
LEFT JOIN DEPARTAMENTO AS D
ON F.Dnr = D.Dnumero
ORDER BY D.Dnome ASC

SELECT F.Unome, D.Dnome
FROM DEPARTAMENTO AS D
LEFT JOIN FUNCIONARIO AS F
ON F.Dnr = D.Dnumero
WHERE F.Cpf IS NULL
ORDER BY D.Dnome ASC
```
---
## Aula 3
- **CONSULTAS: https://github.com/Herysson/Implementacao-de-Banco-de-Dados/blob/main/Aula%2002%20-%20Consultas%20.pdf** *(Programa: SQL Server)*
```
-- Distinct
SELECT DISTINCT F.Salario
FROM FUNCIONARIO AS F;

-- Where
SELECT *
FROM FUNCIONARIO AS F
WHERE F.Pnome = 'Carlos';

-- And
SELECT *
FROM FUNCIONARIO AS F
WHERE F.Sexo = 'M' 
AND F.Salario >= '30000';

-- Or
SELECT *
FROM FUNCIONARIO AS F
WHERE F.Endereco LIKE '%São Paulo%' 
OR F.Endereco LIKE '%Curitiba%';

-- Not 
SELECT *
FROM FUNCIONARIO AS F
WHERE NOT F.Endereco LIKE '%São Paulo%';

-- Order by
SELECT F.Pnome AS 'Nome', F.Unome AS 'Sobrenome', F.Endereco, F.Salario * 12 AS 'CustoAnual'
FROM FUNCIONARIO AS F
ORDER BY CustoAnual DESC;

-- Is null
SELECT *
FROM FUNCIONARIO AS F
WHERE F.Cpf_supervisor IS NULL;

-- Is not null
SELECT *
FROM FUNCIONARIO AS F
WHERE F.Cpf_supervisor IS NOT NULL;

-- Select top (ou "Limit" em MySql) 
SELECT TOP 3 F.Pnome AS 'Nome', F.Unome AS 'Sobrenome', F.Endereco, F.Salario
FROM FUNCIONARIO AS F
ORDER BY F.Salario DESC;

-- Função MIN()
SELECT *
FROM FUNCIONARIO AS F
WHERE F.Salario = (SELECT MIN(Salario) FROM FUNCIONARIO);
    -- ou
DECLARE @salario_min DECIMAL(10, 2);
SET @salario_min = (SELECT MIN(Salario) FROM FUNCIONARIO);
SELECT *
FROM FUNCIONARIO AS F
WHERE F.Salario = @salario_min;

-- Função MAX()
SELECT *
FROM FUNCIONARIO AS F
WHERE F.Salario = (SELECT MAX(Salario) FROM FUNCIONARIO);
    -- ou
DECLARE @salario_max DECIMAL(10, 2);
SET @salario_max = (SELECT MAX(Salario) FROM FUNCIONARIO);
SELECT *
FROM FUNCIONARIO AS F
WHERE F.Salario = @salario_max;

-- Like
SELECT *
FROM FUNCIONARIO AS F
WHERE F.Datanasc LIKE '__72%';

-- In
SELECT F.Pnome AS Nome, T.Pnr AS Projeto, T.Horas
FROM TRABALHA_EM AS T, FUNCIONARIO AS F
WHERE F.Cpf = T.Fcpf
      AND F.Pnome != 'Fernando'
      AND T.Pnr IN (
        SELECT Pnr 
        FROM TRABALHA_EM
        WHERE Fcpf = (
            SELECT CPF 
            FROM FUNCIONARIO 
            WHERE Pnome = 'Fernando'
            )
        );

-- Between
SELECT *
FROM FUNCIONARIO AS F
WHERE F.Salario BETWEEN 30000 AND 40000;
```
- **LIKE:**
<img width="1009" height="447" alt="image" src="https://github.com/user-attachments/assets/45325734-9c82-4a07-873b-7db9803be3d9" />

---
## Aula 2
- **Entidade fraca:** é um componente de banco de dados que não possui atributos suficientes para formar uma chave primária própria, logo ela acaba sendo composta pela chave primária da outra entidade no qual se relaciona (a entidade forte)
  - OBS: *Se a entidade forte é apagada, a entidade fraca é apagada junto, sendo dependente da outra entidade*
<img width="640" height="158" alt="image" src="https://github.com/user-attachments/assets/ab8ed127-e036-4748-94d6-18a581a1e96c" />

- **DDL // Data Definition Language:**
  - **CREATE:** Cria um novo objeto no banco de dados
    - **CREATE SCHEMA ou CREATE DATABASE:** para criar um banco de dados
    - **CREATE TABLE:** para criar uma nova tabela em um banco de dados
  - **ALTER:** Modifica a estrutura do banco de dados
  - **DROP:** Remove objetos do banco de dados
  - **TRUNCATE:** Remove todos os registros de uma tabela

  - **Strings:**
    - **VARCHAR(n):** Ocupa até "n" digitos (máximo 255)
    - **CHAR(n):** Ocupa "n" digitos, os que não forem preenchidos se tornam espaços vazios, mas ainda sendo utilziados
    - **TEXT:** Usado para descrições e textos longos (65k+ de caracteres)
  - **Restrições:**
    - **NOT NULL:** Proibe valores NULL
    - **UNIQUE:** Garante que os valores sejam diferentes
    - **PRIMARY KEY:** Combinação de NOT NULL e UNIQUE
    - **FOREIGN KEY:** Impede ações que destruiriam as ligações entre as tabelas
   
```
-- Criando meu banco
CREATE DATABASE biblioteca;
-- Colocar o banco criado em uso
USE biblioteca;

-- Criando uma tabela
CREATE TABLE autor(
	nome varchar(50) NOT NULL,
    nacionalidade varchar(50) NOT NULL,
    ano_nascimento int NOT NULL,
    idAutor int PRIMARY KEY
);
CREATE TABLE livro(
	titulo text NOT NULL,
    ano_publicacao year NOT NULL,
    idLivro int PRIMARY KEY,
    fk_idAutor int,
    fk_idEditora int
);
CREATE TABLE editora(
	nome varchar(50) NOT NULL,
    cidade varchar(50) NOT NULL,
    site varchar(100),
    ano_fundacao int NOT NULL,
    idEditora int PRIMARY KEY
);

-- Exibe as tabelas do banco
SHOW TABLES;
-- Exibe metadados da tabela
DESC autor;

-- Adicionando FK via alteração 1
ALTER TABLE livro
ADD CONSTRAINT fk_Autor -- nome da restrição
FOREIGN KEY (fk_idAutor) REFERENCES autor(idAutor);
-- Adicionando FK via alteração 2
ALTER TABLE livro
ADD CONSTRAINT fk_Editora
FOREIGN KEY (fk_idEditora) REFERENCES editora(idEditora);

-- Adicionando uma nova coluna
ALTER TABLE livro
ADD genero varchar(50) NOT NULL;
-- Remover uma coluna
ALTER TABLE livro
DROP COLUMN genero;

-- Modificar o tipo de dado de uma coluna
ALTER TABLE autor
MODIFY COLUMN nacionalidade char(2);

-- Alterando o nome de uma coluna
ALTER TABLE livro
CHANGE idLivro ISBN char(13);

-- Inserindo valores
INSERT INTO autor
VALUES 	("Machado de Assis", "BR", 1839, 101),
		("George Orwell", "UK", 1903, 102),
        ("Juca da Silva", "BR", 2010, 103);
INSERT INTO editora
VALUES	("Companhia das Letras", "São Paulo", "www.cdl.br", 1986, 201),
		("Penguin", "Londres", "www.pg.ldn", 1935, 202);
INSERT INTO livro
VALUES  ("Dom Casmurro", 1901, "9874689", 101, 301),
		("1984", 1949, "9500234", 102, 302);
        
-- Recuperando as informações
SELECT * FROM autor;

-- Deletando um valor
DELETE FROM autor
WHERE autor.idAutor = 103;

-- Alterando um valor
UPDATE autor
SET autor.nacionalidade = "US"
WHERE autor.idAutor = 103;

-- Selecionado e exibindo informações de uma tabela 1
SELECT l.titulo, l.ano_publicacao
FROM livro AS l
WHERE l.titulo LIKE "%Dom%";
-- Selecionado e exibindo informações de uma tabela 2
SELECT l.titulo AS "Título", l.ano_publicacao AS "Ano", CONCAT(a.nome, "/", a.nacionalidade) AS "Autor/Nasc", e.nome AS "Editora"
FROM livro AS l
JOIN autor AS a ON l.fk_idAutor = a.idAutor
JOIN editora AS e ON l.fk_idEditora = e.idEditora;
```
<img width="534" height="258" alt="image" src="https://github.com/user-attachments/assets/6326851a-2b49-474d-b406-2ff7c19e4670" />

- **DML // Data Manipulation Language:**
	- **INSERT INTO:** Insere valores em uma coluna
		- *INSERT INTO nome_tabela (coluna1, coluna2, coluna3, ...)*
		- *VALUES (valor1, valor2, valor3, ...);*
	- **SELECT:** Seleciona informações de uma tabela
  		- *SELECT -> FROM -> WHERE*
      		- SELECT (lista de atributos)
          	- FROM (lista de tabelas)
          	- WHERE (condição)
  				- ```=, >, <, >=, <=, <> ou !=, BETWEEN, LIKE, AND, OR```
 	- **DELETE FROM/UPDATE:** Deleta/Atualiza valores de uma tabela
		- *[!] NÃO UTILIZAR SEM A CLÁUSULA "WHERE"*
---
## Aula 1
### Programa utilizado: brModelo.jar
- **Revisão de Banco de Dados:** https://github.com/Herysson/Implementacao-de-Banco-de-Dados/blob/main/Aula%2000%20-%20Boas%20pr%C3%A1ticas.md
- **Chave primária natural:** faz parte da entidade (ex: CPF, email)
- **Atributo multivalorado:** atributo que a pessoa pode ter um ou mais registrado (ex: telefone)
- **Atributo monovalorado:** atributo que a pessoa só pode ter um (ex: CPF)
- **Diagrama lógico:** representa estrutura física do banco de dados
- **Chave estrangeira:** sempre é puxada para a entidade N
- **Entidade associativa:** gerada quando ocorre relacionamento N..N, puxando as chaves primárias das entidades, criando uma chave primária composta
- **Candidatos a entidade:** se houver muita duplicidade (ex: mais de um autor, mais de uma categoria, muita repetição (não é algo único))

### **Modelo Conceitual:**
<img width="935" height="635" alt="image" src="https://github.com/user-attachments/assets/ff356e51-4a54-46c1-b522-182de3accb26" />

### **Modelo Lógico:**
<img width="704" height="653" alt="image" src="https://github.com/user-attachments/assets/e93094f1-98ba-46f4-bacc-1a6bf592ce54" />



