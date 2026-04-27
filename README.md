# Catalogo de Produtos - Spring Boot + PostgreSQL

Este projeto foi desenvolvido com:

- Java 17
- Spring Boot 3
- Maven Wrapper (`mvnw`)
- PostgreSQL
- Thymeleaf

## 1. Pre-requisitos

Antes de rodar, instale:

- JDK 17
- PostgreSQL (servidor ativo)

## 2. Criar banco de dados no PostgreSQL

Abra o PostgreSQL (pgAdmin, DBeaver ou terminal SQL) e execute:

```sql
CREATE DATABASE catalogo;
```

Opcional: se quiser usar outro nome de banco, basta ajustar no `application.properties`.

## 3. Configurar o `application.properties`

Arquivo:

`src/main/resources/application.properties`

Exemplo de configuração:

```properties
spring.application.name=appdb

# PostgreSQL
spring.datasource.url=jdbc:postgresql://localhost:5432/catalogo
spring.datasource.username=postgres
spring.datasource.password=123456
spring.datasource.driver-class-name=org.postgresql.Driver

# JPA
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

### O que ajustar nesse arquivo

- `spring.datasource.url`: host, porta e nome do banco.
- `spring.datasource.username`: usuario do PostgreSQL.
- `spring.datasource.password`: senha do PostgreSQL.

## 4. Rodar o projeto

No terminal, dentro da pasta raiz do projeto (onde está o `pom.xml`), execute:

```bash
./mvnw spring-boot:run
```

No Windows (PowerShell/CMD):

```bat
mvnw.cmd spring-boot:run
```

A aplicação sobe por padrão em:

- `http://localhost:8080`

## 5. Usuarios padrao criados automaticamente

Na primeira execução, o projeto tenta criar os usuarios:

- `usuario` / `usuario@123` (perfil `ROLE_USER`)
- `adm` / `adm@123` (perfil `ROLE_ADMIN`)

Observacao importante:

- Se já existirem usuarios antigos (exemplo: `joao` e `arthur`) no banco, eles nao sao apagados automaticamente.
- O projeto apenas adiciona os novos usuarios se ainda nao existirem.

## 6. Erros comuns e como resolver

### Erro de conexão com banco

Verifique:

- Se o PostgreSQL está iniciado.
- Se `username` e `password` estão corretos.
- Se o banco informado na URL existe.
- Se a porta (`5432`) está correta.

### Porta 8080 em uso

Você pode mudar a porta no `application.properties`:

```properties
server.port=8081
```

## 7. Observacao para avaliacao/professor

Este projeto usa `spring.jpa.hibernate.ddl-auto=update`, portanto as tabelas sao criadas/atualizadas automaticamente conforme as entidades Java, sem necessidade de script manual para estrutura inicial.
