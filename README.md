# Implementação de Banco de Dados
---
## Aula 2
- **Entidade fraca:** é um componente de banco de dados que não possui atributos suficientes para formar uma chave primária própria, logo ela acaba sendo composta pela chave primária da outra entidade no qual se relaciona (a entidade forte)
  - *Se a entidade forte é apagada, a entidade fraca é apagada junto, sendo dependente da outra entidade*
<img width="640" height="158" alt="image" src="https://github.com/user-attachments/assets/ab8ed127-e036-4748-94d6-18a581a1e96c" />

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



