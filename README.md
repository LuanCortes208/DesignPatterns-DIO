# DesignPatterns-DIO

# Task Board API

Este projeto implementa uma API REST para gerenciamento de um quadro de tarefas (task board) utilizando Spring Boot e banco de dados H2 em memória.

## Estrutura do Projeto

O projeto está estruturado seguindo o padrão de camadas:

```
src/main/java/com/taskboard
│
├── config/                   # Configurações do Spring Boot
├── controller/               # Controladores REST 
├── dto/                      # Data Transfer Objects
├── entity/                   # Entidades JPA
├── repository/               # Interfaces de acesso ao banco
├── service/                  # Lógica de negócio
└── exception/                # Classes de exceção personalizadas
```

## Configuração e Execução

### Requisitos

- Java 17 ou superior
- Maven 3.8.x ou superior

### Como executar

1. Clone o repositório
2. Navegue até a pasta do projeto
3. Execute o comando:

```bash
./mvnw spring-boot:run
```

Ou importe o projeto em sua IDE favorita (IntelliJ, Eclipse, VSCode) e execute a classe `TaskBoardApplication`.

### Acessando o H2 Console

O H2 Console está habilitado e pode ser acessado em:

```
http://localhost:8080/h2-console
```

Credenciais (conforme definido em application.properties):
- JDBC URL: `jdbc:h2:mem:taskdb`
- Username: `sa`
- Password: `password`

## API Endpoints

### Criar uma Tarefa

**POST** `/api/tasks`

Exemplo de payload:
```json
{
  "title": "Implementar autenticação",
  "description": "Adicionar JWT para autenticação de usuários",
  "status": "TODO"
}
```

### Listar Todas as Tarefas

**GET** `/api/tasks`

### Buscar uma Tarefa por ID

**GET** `/api/tasks/{id}`

### Atualizar uma Tarefa

**PUT** `/api/tasks/{id}`

Exemplo de payload:
```json
{
  "title": "Implementar autenticação",
  "description": "Adicionar JWT para autenticação de usuários",
  "status": "DOING"
}
```

### Atualizar Status de uma Tarefa

**PATCH** `/api/tasks/{id}/status`

Exemplo de payload:
```json
{
  "status": "DONE"
}
```

### Deletar uma Tarefa

**DELETE** `/api/tasks/{id}`

## Adaptando para Outros Bancos de Dados

Para adaptar este projeto para utilizar PostgreSQL ou outro banco de dados relacional:

1. Adicione a dependência apropriada no `pom.xml`:

```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
</dependency>
```

2. Modifique as configurações no `application.properties`:

```properties
# PostgreSQL
spring.datasource.url=jdbc:postgresql://localhost:5432/taskboard
spring.datasource.username=postgres
spring.datasource.password=sua_senha
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
```

3. Remova as configurações específicas do H2:

```properties
# Remover ou comentar
# spring.h2.console.enabled=true
# spring.h2.console.path=/h2-console
```

4. Os scripts de migração (se estiver usando Flyway ou Liquibase) podem precisar de pequenos ajustes para compatibilidade com a sintaxe do PostgreSQL.

## Possíveis Melhorias

- Adicionar autenticação e controle de acesso
- Implementar agrupamento de tarefas por projetos
- Adicionar funcionalidade de atribuição de tarefas a usuários
- Implementar notificações para tarefas próximas do prazo
