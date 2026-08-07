# Implementação de Banco de Dados
---
## Aula 2
- **Entidade fraca:** é um componente de banco de dados que não possui atributos suficientes para formar uma chave primária própria, logo ela acaba sendo composta pela chave primária da outra entidade no qual se relaciona (a entidade forte)
  - OBS: *Se a entidade forte é apagada, a entidade fraca é apagada junto, sendo dependente da outra entidade*
<img width="640" height="158" alt="image" src="https://github.com/user-attachments/assets/ab8ed127-e036-4748-94d6-18a581a1e96c" />

- **DDL: Data Definition Language:**
  - **CREATE:** Cria um novo objeto no banco de dados
    - **CREATE SCHEMA ou CREATE DATABASE:** para criar um banco de dados
    - **CREATE TABLE:** para criar uma nova tabela em um banco de dados
  - **ALTER:** Modifica a estrutura do banco de dados
  - **DROP:** Remove objetos do banco de dados
  - **TRUNCATE:** Remove todos os registros de uma tabela

  - **STRINGS:**
    - **VARCHAR(n):** Ocupa até "n" digitos (máximo 255)
    - **CHAR(n):** Ocupa "n" digitos, os que não forem preenchidos se tornam espaços vazios, mas ainda sendo utilziados
    - **TEXT:** Usado para descrições e textos longos (65k+ de caracteres)
  - **Restrições:**
    - **NOT NULL:** Proibe valores NULL
    - **UNIQUE:** Garante que os valores sejam diferentes
    - **PRIMARY KEY:** Combinação de NOT NULL e UNIQUE
    - **FOREIGN KEY:** Impede ações que destruiriam as ligações entre as tabelas

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



