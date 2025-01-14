# Backend
Codigo del backend de la pagina web
## Creación del project

Cargar el navegador y generar un proyecto Spring a partir del siguiente enlace:

https://start.spring.io/#!type=maven-project&language=java&platformVersion=3.2.5&packaging=jar&jvmVersion=21&groupId=pe.edu.upc.learning&artifactId=learning-center-platform&name=learning-center-platform&description=Demo%20project%20for%20Spring%20Boot&packageName=pe.edu.upc.learning.platform&dependencies=data-jpa,validation,web,modulith,devtools,postgresql,lombok 

Generar el project Spring, Guardarlo en la carpeta IdeaProject y luego abrirlo el IntellIJIdea.

## Base de datos

Abrir pgAdmin y crear la base de datos: `aymcomputersolutions`.

## application.properties

Abrir el archivo `application.properties` y agregar el siguiente código:
```
server.port: 8090

### PostgreSQL
spring.datasource.driver-class-name: org.postgresql.Driver
###    JDBC : SGDB :// HOST : PORT / DB
spring.datasource.url: jdbc:postgresql://localhost:5432/aymcomputersolutions
spring.datasource.username: postgres
spring.datasource.password: 1234

spring.jpa.database: postgresql
spring.jpa.hibernate.ddl-auto: update
spring.jpa.show-sql: true

spring.jpa.properties.hibernate.format_sql: true
spring.jpa.properties.hibernate.dialect: org.hibernate.dialect.PostgreSQLDialect
```

## Project structur for shared

En el package principal `pe.edu.upc.aymcomputersolutions.platform`, crear la siguiente estructura para el package `shared` :file_folder: .

```markdown
- 📁 shared
  - 📁 domain.model.entities
    - 📄 AuditableModel.java
  - 📁 infrastructure
    - 📁 documentation.openapi.configuration
    - 📁 persistence.jpa.strategy
  - 📁 interfaces.rest.resources
    - 📄 MessageResource.java
```

En el package `domain.model.entities` crear la clase `AuditableModel` con el siguiente contenido:

```java
import jakarta.persistence.Column;
import jakarta.persistence.EntityListeners;
import jakarta.persistence.MappedSuperclass;
import lombok.Data;
import org.springframework.data.annotation.CreatedDate;
import org.springframework.data.annotation.LastModifiedDate;
import org.springframework.data.jpa.domain.support.AuditingEntityListener;

import java.util.Date;

@EntityListeners(AuditingEntityListener.class)
@MappedSuperclass
@Data
public class AuditableModel {

    @CreatedDate
    @Column(nullable = false, updatable = false)
    private Date createdAt;

    @LastModifiedDate
    @Column(nullable = false)
    private Date updatedAt;
}
```

En el package `interfaces.rest.resources` crear el record `MessageResource` con el siguiente contenido:
```java
public record MessageResource(String message) {
}
```

## Project structur for Learning Bounded Context

Crear la siguiente estructura para el Bounded Context ` `:

```markdown
- 📁 learning
  - 📁 application.internal
    - 📁 commandservices
    - 📁 eventhandlers
    - 📁 outboundservices.acl
    - 📁 queryservices
  - 📁 domain
    - 📁 exceptions
    - 📁 model
      - 📁 aggregates
      - 📁 commands
      - 📁 entities
      - 📁 events
      - 📁 queries
      - 📁 valueobjects
    - 📁 services
  - 📁 infrastructure.persistence.jpa.repositories
  - 📁 interfaces.rest
    - 📁 resources
    - 📁 transform
```
