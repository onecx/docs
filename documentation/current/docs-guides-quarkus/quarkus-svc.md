# Backend service (svc)

## [](#%5Fproject%5Fsetup)Project setup

Now that [project structure](project-structure.html) is set up for the Onecx Quarkus project, we can configure the backend service and extend the project configuration.

### [](#%5Fparent%5Fconfiguration)Parent configuration

Project maven parent configuration, artifactId and project version.

| |  More information about maven parent pom pattern [Apache Maven Pom Documentation](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html) |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Maven parent configuration

```xml
<parent>
    <groupId>org.tkit.onecx</groupId>
    <artifactId>onecx-quarkus3-parent</artifactId>
    <version>0.72.0</version>
</parent>
```

### [](#%5Fdependencies)Dependencies

| |  All version of the dependencies are defined in the parent project. Project itself should not define any version of these dependencies. |
| ----------------------------------------------------------------------------------------------------------------------------------------- |

By default, we will have the following maven dependencies:

* [tkit-quarkus](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/index.html) are quarkus extensions for `JPA`, `log`, `json-log` and `rest-log`
* [quarkus](https://quarkus.io/guides/) cloud native extensions (health, metrics, tracing, …​), quarkus-rest, hibernate-orm and liquibase
* [lombok](https://projectlombok.org/) to generate getters, setters and much more
* [mapstruct](https://mapstruct.org/documentation/stable/reference/html/) Generator to generate a source that maps `DTO` to `JPA` models and vice versa

Backend service default dependencies 

```xml
<dependencies>
        <!-- ONECX -->

        <!-- 1000kit -->
        <dependency>
            <groupId>org.tkit.quarkus.lib</groupId>
            <artifactId>tkit-quarkus-rest-context</artifactId>
        </dependency>
        <dependency>
            <groupId>org.tkit.quarkus.lib</groupId>
            <artifactId>tkit-quarkus-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>org.tkit.quarkus.lib</groupId>
            <artifactId>tkit-quarkus-log-cdi</artifactId>
        </dependency>
        <dependency>
            <groupId>org.tkit.quarkus.lib</groupId>
            <artifactId>tkit-quarkus-log-rs</artifactId>
        </dependency>
        <dependency>
            <groupId>org.tkit.quarkus.lib</groupId>
            <artifactId>tkit-quarkus-log-json</artifactId>
        </dependency>
        <dependency>
            <groupId>org.tkit.quarkus.lib</groupId>
            <artifactId>tkit-quarkus-rest</artifactId>
        </dependency>

        <!-- QUARKUS -->
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-arc</artifactId>
        </dependency>
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-liquibase</artifactId>
        </dependency>
        <dependency>
            <groupId>com.github.blagerweij</groupId>
            <artifactId>liquibase-sessionlock</artifactId>
        </dependency>
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-smallrye-health</artifactId>
        </dependency>
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-micrometer-registry-prometheus</artifactId>
        </dependency>
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-hibernate-orm</artifactId>
        </dependency>
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-resteasy-reactive</artifactId>
        </dependency>
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-resteasy-reactive-jackson</artifactId>
        </dependency>
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-jdbc-postgresql</artifactId>
        </dependency>
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-smallrye-context-propagation</artifactId>
        </dependency>
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-smallrye-openapi</artifactId>
        </dependency>
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-hibernate-validator</artifactId>
        </dependency>
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-opentelemetry</artifactId>
        </dependency>

        <!-- OTHER -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mapstruct</groupId>
            <artifactId>mapstruct</artifactId>
        </dependency>
</dependencies>
```

### [](#%5Fgenerate%5Frest%5Fendpoint)Generate rest endpoint

In `onecx` project we do use API-first approach. First we need to defined our `REST` interface with `openApi`. Create a `example-v1.yaml` (pattern: <application>-<version>.yaml) in the `src/main/openapi` directory.

Please taken into account the [API Guidelines](../onecx-docs-dev/guidelines/api%5Fguidelines.html).

Now we can configure `org.tkit.onecx.quarkus:onecx-openapi-generator` Maven plugin. The important part of the Maven plugin is xml configuration element.

OpenApi generator full Maven plugin configuration

```xml
<plugin>
    <groupId>org.openapitools</groupId>
    <artifactId>openapi-generator-maven-plugin</artifactId>
    <configuration>
        <generatorName>jaxrs-spec</generatorName>
        <modelNameSuffix>DTO</modelNameSuffix>
        <generateApiTests>false</generateApiTests>
        <generateApiDocumentation>false</generateApiDocumentation>
        <generateModelTests>false</generateModelTests>
        <generateModelDocumentation>false</generateModelDocumentation>
        <generateSupportingFiles>false</generateSupportingFiles>
        <addCompileSourceRoot>true</addCompileSourceRoot>
        <library>quarkus</library>
        <additionalProperties>onecx-scopes=true</additionalProperties>
        <configOptions>
            <sourceFolder>/</sourceFolder>
            <openApiNullable>false</openApiNullable>
            <returnResponse>true</returnResponse>
            <useTags>true</useTags>
            <interfaceOnly>true</interfaceOnly>
            <serializableModel>true</serializableModel>
            <singleContentTypes>true</singleContentTypes>
            <dateLibrary>java8</dateLibrary>
            <useMicroProfileOpenAPIAnnotations>true</useMicroProfileOpenAPIAnnotations>
            <useJakartaEe>true</useJakartaEe>
            <useBeanValidation>true</useBeanValidation>
            <java17>true</java17>
        </configOptions>
    </configuration>
    <executions>
        <execution>
            <id>internal</id>
            <goals>
                <goal>generate</goal>
            </goals>
            <configuration>
                <inputSpec>src/main/openapi/onecx-theme-internal-openapi.yaml</inputSpec>
                <apiPackage>gen.org.tkit.onecx.theme.rs.internal</apiPackage>
                <modelPackage>gen.org.tkit.onecx.theme.rs.internal.model</modelPackage>
                <modelNameSuffix>DTO</modelNameSuffix>
            </configuration>
        </execution>
    </executions>
</plugin>
```

After we run `mvn clean package` maven plugin will generate in corresponding source code in `target/generated-sources` directory.

### [](#%5Frest%5Fimplementation)REST Implementation

To implement the `RoleRestController` we need to create a java class which implements generated interface `gen.org.tkit.onecx.example.rs.v1.RoleInternalApi`.

RoleRestController 

```java
import jakarta.enterprise.context.ApplicationScoped;
import jakarta.ws.rs.core.Response;
import jakarta.validation.ConstraintViolationException;
import org.tkit.quarkus.jpa.exceptions.ConstraintException;
import jakarta.persistence.OptimisticLockException;

import gen.org.tkit.onecx.example.rs.v1.RoleInternalApi;
import gen.org.tkit.onecx.example.rs.v1.model.CreateRoleRequestDTO;

@ApplicationScoped
public class RoleRestController implements RoleInternalApi {

    @Inject
    RoleMapper mapper;

    @Inject
    ExceptionMapper exceptionMapper;

    @Context
    UriInfo uriInfo;

    @Override
    public Response createRole(CreateRoleRequestDTO createRoleRequestDTO) {
        var role = mapper.create(createRoleRequestDTO);
        role = dao.create(role);
        return Response
                .created(uriInfo.getAbsolutePathBuilder().path(role.getId()).build())
                .entity(mapper.map(theme))
                .build();
    }

    // constraint exception exception handler
    @ServerExceptionMapper
    public RestResponse<ProblemDetailResponseDTO> exception(ConstraintException ex) {
        return exceptionMapper.exception(ex);
    }

    // constraint violation exception handler
    @ServerExceptionMapper
    public RestResponse<ProblemDetailResponseDTO> constraint(ConstraintViolationException ex) {
        return exceptionMapper.constraint(ex);
    }

    // Optimistic lock exception handler
    @ServerExceptionMapper
    public RestResponse<ProblemDetailResponseDTO> optimisticLockException(OptimisticLockException ex) {
        return exceptionMapper.optimisticLock(ex);
    }

}
```

For the backend service we need to define exception mapper methods for following exception:

* `jakarta.persistence.OptimisticLockException` \- this exception is throw when try to store object in the database with old or wrong `OPTLOCK` number.
* `jakarta.validation.ConstraintViolationException` \- when we activate a validation framework `io.quarkus:quarkus-hibernate-validator` this exception will be thrown when request does not match to the requirements defined in the OpenApi.
* `org.tkit.quarkus.jpa.exceptions.ConstraintException` \- this exception will be thrown for any database constraints.

| |  With the annotation @ServerExceptionMapper we defined the exception mapper for each Exception in the context of the RestController. |
| -------------------------------------------------------------------------------------------------------------------------------------- |

To map the request `DTO` object to the `JPA` model we use the `Mapstruct`. We define the `RoleMapper` in our example.

```java
import org.tkit.quarkus.rs.mappers.OffsetDateTimeMapper;

@Mapper(uses = { OffsetDateTimeMapper.class })
public interface RoleMapper {

    @Mapping(target = "id", ignore = true)
    @Mapping(target = "creationDate", ignore = true)
    @Mapping(target = "creationUser", ignore = true)
    @Mapping(target = "modificationDate", ignore = true)
    @Mapping(target = "modificationUser", ignore = true)
    @Mapping(target = "controlTraceabilityManual", ignore = true)
    @Mapping(target = "modificationCount", ignore = true)
    @Mapping(target = "persisted", ignore = true)
    @Mapping(target = "tenantId", ignore = true)
    Role create(CreateRoleRequestDTO dto);

    // ... more mapping methods
}
```

The same approach we use for the exception mapper which could be shared between multiple `RestController` for the same rest interface.

```java
import org.tkit.quarkus.rs.mappers.OffsetDateTimeMapper;

@Mapper(uses = { OffsetDateTimeMapper.class })
public interface ExceptionMapper {

    default RestResponse<ProblemDetailResponseDTO> constraint(ConstraintViolationException ex) {
        var dto = exception(ErrorKeys.CONSTRAINT_VIOLATIONS.name(), ex.getMessage());
        dto.setInvalidParams(createErrorValidationResponse(ex.getConstraintViolations()));
        return RestResponse.status(Response.Status.BAD_REQUEST, dto);
    }

    //.... more mapping methods
}
```

| |  org.tkit.quarkus.rs.mappers.OffsetDateTimeMapper mapper is predefined a mapstruct mapper for OffsetDateTime and LocalDateTime object. |
| ---------------------------------------------------------------------------------------------------------------------------------------- |

### [](#%5Fjpa%5Flayer%5Fimplementation)JPA layer implementation

For our project we will use the `tkit-quarkus-jpa` and `tkit-quarkus-jpa-models` extension for Quarkus which have simple API on top of JPA. We have abstract `DAO` classes and abstract Entity classes which provides basic `CRUD` operation. For more information please read the extension [tkit-quarkus-jpa](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/index.html) documentation.

```xml
<dependency>
    <groupId>org.tkit.quarkus.lib</groupId>
    <artifactId>tkit-quarkus-jpa</artifactId>
</dependency>
```

Create User entity class in the `org.tkit.onecx.user.domain.models` package. The entity class extend the `TraceableEntity`. In the entity class can use the Lombok annotation `@Getter` and `@Setter` to generate the getters and setters.

Example user entity 

```java
import javax.persistence.Entity;
import javax.persistence.Table;
import org.tkit.quarkus.jpa.models.TraceableEntity;

@Entity
@Table(name = "T_USER")
public class User extends TraceableEntity {

    @Column(name = "USERNAME")
    private String username;
}
```

Example user DAO 

```java
import org.tkit.quarkus.jpa.daos.AbstractDAO;
import javax.enterprise.context.ApplicationScoped;

@ApplicationScoped
public class UserDAO extends AbstractDAO<User> {

}
```

#### [](#%5Fdatabase%5Fconfiguration)Database configuration

In `onecx` project we do use the `postgresql` database for our backend services.

```properties
quarkus.datasource.db-kind=postgresql
quarkus.datasource.jdbc.max-size=30
quarkus.datasource.jdbc.min-size=10

quarkus.hibernate-orm.database.generation=validate
quarkus.hibernate-orm.jdbc.timezone=UTC
quarkus.liquibase.migrate-at-start=true
quarkus.liquibase.validate-on-migrate=true
```

| |  The parameter quarkus.hibernate-orm.log.sql will activate the hibernate logs in the console. |
| ----------------------------------------------------------------------------------------------- |

#### [](#%5Fdatabase%5Fschema%5Fchange%5Fmanagement)Database schema change management

[Liquibase](https://www.liquibase.com/) is an open source tool for database schema change management. We will this framework in our example. Liquibase does have abstraction layer xml, json or yaml to support multi databases. Liquibase can generate the changes and compare our Hibernate model with existing database.

For the database schema change management we do use [quarkus-liquibase](https://quarkus.io/guides/) extension. To generate a database changes or validate the database changes we do use [tkit-liquibase-plugin](https://github.com/1000kit/tkit-liquibase-plugin) which is configured in the onecx-quarkus3-parent.

Quarkus liquibase configuration

```properties
quarkus.liquibase.migrate-at-start=true
quarkus.liquibase.validate-on-migrate=true
```

By default, liquibase does not use session lock. To activate the liquibase session lock during the start of our service we do use `com.github.blagerweij:liquibase-sessionlock` liquibase extension. No configuration is need to this extension.

To generate the database changes run following command

```shell
mvn clean compile -Pdb-diff
```

To check if you are missing any changes run following command

```shell
mvn validate -Pdb-check
```

#### [](#%5Fjpa%5Fdate%5Ftime)JPA date-time

First, you need to configure the database server to use the UTC timezone. For example PostgreSQL default is UTC. Second, you need to set hibernate.jdbc.time\_zone Hibernate property to the value of UTC. For the Quarkus application we need set key quarkus.hibernate-orm.jdbc.timezone to UTC value in the application.properties.

```properties
quarkus.hibernate-orm.jdbc.timezone=UTC
```

The date representation in the database is store in the UTC as long number. Date fields in the JPA entity represents this database date as LocalDateTime. On the another hand the DTO represents the date as ISO text. To get it running we need to create a mapper which will map the LocalDateTime to OffsetDatetime. In the mapping we should not lose the Offset/Zone information.

| |  The date representation in the JPA entity is the LocalDateTime java type and in the DTO object is the OffsetDateTime java type. |
| ---------------------------------------------------------------------------------------------------------------------------------- |

Example user entity 

```java
@Entity
@Table(name = "T_USER")
public class User extends TraceableEntity {
    private String username;
    private LocalDateTime date;
}
```

Example user DTO 

```java
@RegisterForReflection
public class UserDTO extends TraceableDTO {
    private String username;
    private OffsetDateTime date;
}
```

Example user mapper 

```java
import org.tkit.quarkus.rs.mappers.OffsetDateTimeMapper;

@Mapper(uses = OffsetDateTimeMapper.class)
public interface UserMapper {

    UserDTO map(User model);

    User create(UserDTO dto);
}
```

In the tests we need to configure the RestAssured to use text representation of the date-time.

```java
public abstract class AbstractTest {
    static {
        RestAssured.config = RestAssuredConfig.config().objectMapperConfig(
            ObjectMapperConfig.objectMapperConfig().jackson2ObjectMapperFactory(
                (cls, charset) -> {
                     ObjectMapper objectMapper = new ObjectMapper();
                     objectMapper.registerModule(new JavaTimeModule());
                     objectMapper.configure(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS, false);
                     return objectMapper;
                }
            )
        );
    }
}
```

### [](#%5Fjpa%5Fcustom%5Fbusiness%5Fid)JPA custom business ID

#### [](#%5Fpostgressql%5Fserial%5Ftype)PostgresSQL SERIAL type

```java
@GeneratorType(type = BidStringGenerator.class, when = GenerationTime.INSERT)
@Column(name = "CUSTOM")
String custom;
```

#### [](#%5Fgeneric%5Fsequence%5Fimplementation)Generic sequence implementation

```java
import javax.persistence.Column;
import org.my.group.BusinessId;

@BusinessId(sequence = "SEQ_MY_ENTITY_BID")
@Column(name = "bid_anno")
Long bid;
```

Follow the implementation of the custom annotation `BusinessId`.

BusinessId 

```java
import org.hibernate.annotations.ValueGenerationType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;

@ValueGenerationType(generatedBy = BusinessIdValueGeneration.class)
@Retention(RetentionPolicy.RUNTIME)
public @interface BusinessId {

    String sequence() default "";

}
```

BusinessIdValueGeneration 

```java
import org.hibernate.tuple.AnnotationValueGeneration;
import org.hibernate.tuple.GenerationTiming;
import org.hibernate.tuple.ValueGenerator;

public class BusinessIdValueGeneration implements AnnotationValueGeneration<BusinessId> {

    String sequence;

    @Override
    public void initialize(BusinessId annotation, Class<?> propertyType) { sequence = annotation.sequence(); }

    @Override
    public GenerationTiming getGenerationTiming() { return GenerationTiming.INSERT; }

    @Override
    public ValueGenerator<?> getValueGenerator() { return new BusinessIdGenerator(sequence); }

    @Override
    public boolean referenceColumnInSql() { return false; }

    @Override
    public String getDatabaseGeneratedReferencedColumnValue() { return null; }
}
```

BusinessIdGenerator 

```java
import org.hibernate.Session;
import org.hibernate.internal.SessionFactoryImpl;
import org.hibernate.jdbc.ReturningWork;
import org.hibernate.tuple.ValueGenerator;

import java.sql.PreparedStatement;
import java.sql.ResultSet;


public class BusinessIdGenerator implements ValueGenerator<Long> {

    String sequence;

    BusinessIdGenerator(String sequence) {
        this.sequence = sequence;
    }

    @Override
    public Long generateValue(Session session, Object owner) {
        SessionFactoryImpl sessionFactory = (SessionFactoryImpl) session.getSessionFactory();
        String sql = sessionFactory.getJdbcServices().getDialect().getSequenceNextValString(sequence);
        ReturningWork<Long> seq = connection -> {
            try (PreparedStatement preparedStatement = connection.prepareStatement(sql);
                 ResultSet resultSet = preparedStatement.executeQuery()) {
                resultSet.next();
                return resultSet.getLong(1);
            }
        };
        return sessionFactory.getCurrentSession().doReturningWork(seq);
    }
}
```

We need to add the sequence to the `import.sql` for the local development.

```sql
CREATE SEQUENCE IF NOT EXISTS seq_my_entity_bid;
```

#### [](#%5Fcustom%5Fin%5Fmemory%5Fgenerator)Custom in-Memory generator

```java
@GeneratorType(type = BidStringGenerator.class, when = GenerationTime.INSERT)
@Column(name = "CUSTOM")
String custom;
```

Follow the implementation of the custom generator `BidStringGenerator`.

```java
public class BidStringGenerator implements ValueGenerator<String> {

    @Override
    public String generateValue(Session session, Object owner) {
        MyEntity e = (MyEntity) owner;
        return e.name + "+" + UUID.randomUUID();
    }
}
```

### [](#%5Ftests)Tests

For the test we add following dependencies to our project

Test dependencies 

```xml
<dependencies>
    <!-- TEST -->
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-junit5</artifactId>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-junit5-mockito</artifactId>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>io.rest-assured</groupId>
        <artifactId>rest-assured</artifactId>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.tkit.quarkus.lib</groupId>
        <artifactId>tkit-quarkus-test-db-import</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

| |  The Quarkus tests has support for the injection and mocking. This will work only for the Quarkus JVM tests and not for native image test or integration tests with a docker image. Try to avoid this in our tests to have much more reusable tests. In most cases, the mock service also fakes code to pass the test. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

For our test we will use this pattern for the test classes

* `<Name>RestControllerTest extends AbstractTest` \- the extended test for the common and unit test. For example: UserRestControllerTest
* `<Name>RestControllerTestIT extends <Name>RestControllerTest` \- the extended test for the integration test. For example: UserRestControllerTestIT

The 1000kit test extension `tkit-quarkus-test-db-import` does have support to import test data for the tests during the test execution. We will create our test data as `XML` data. Store the xml file in the `src/test/resources/data` directory under name `test-internal.xml`. The magic is in the `@WithDBData` annotation which could be used on the `Class` or `Method` level. Example of the xml test data file:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<dataset>
    <ROLE guid="r21" optlock="0" name="n1" />
    <ROLE guid="r22" optlock="0" name="n2" />
</dataset>
```

| |  Only the XML DbUnit FlatXmlDataSet format is supported. |
| ---------------------------------------------------------- |

Example of the `RoleRestControllerTest` class.

```java
@QuarkusTest
@TestHTTPEndpoint(RoleRestController.class)
@WithDBData(value = "data/test-internal.xml", deleteBeforeInsert = true, deleteAfterTest = true, rinseAndRepeat = true)
class RoleRestControllerTest extends AbstractTest {

    @Test
    void getRoleByIdTest() {

        // get role by ID
        var dto = given().contentType(APPLICATION_JSON).get("r12")
                .then().statusCode(OK.getStatusCode()).contentType(APPLICATION_JSON)
                .extract().body().as(RoleDTO.class);

        // validate role
        assertThat(dto).isNotNull();
        assertThat(dto.getName()).isEqualTo("n2");
        assertThat(dto.getId()).isEqualTo("r12");

        // not found
        given().contentType(APPLICATION_JSON).get("___").then().statusCode(NOT_FOUND.getStatusCode());
    }
}
```

Example of the role rest controller integration test.

```java
import io.quarkus.test.junit.QuarkusIntegrationTest;

@QuarkusIntegrationTest
class RoleRestControllerTestIT extends RoleRestControllerTest {

}
```

### [](#%5Fsecurity)Security

To enable scope security for backend services we need to add these Maven dependencies.

```xml
<dependencies>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-oidc</artifactId>
    </dependency>
    <dependency>
        <groupId>org.tkit.onecx.quarkus</groupId>
        <artifactId>onecx-security</artifactId>
    </dependency>
</dependencies>
```

The next step is to add the `OAuth` scopes to our OpenApi definition. In our example, we add the `read` scope to the `createRole` method.

Example openapi with scope 

```yaml
openapi: 3.0.3
info:
  title: example service
  version: 1.0.0
servers:
  - url: "http://onecx-example-svc:8080"
paths:
  /internal/roles:
    get:
      security:
        - oauth2: [read]
      operationId: createRole
      responses:
        201:
          description: "Role created"
components:
  securitySchemes:
    oauth2:
      type: oauth2
      flows:
        clientCredentials:
          tokenUrl: https://oauth.simple.api/token
          scopes:
            read: Grants read access
```

Now we need to add the extension `org.tkit.onecx.quarkus:onecx-openapi-generator` which will generate the Quarkus annotation `@io.quarkus.security.PermissionsAllowed` for the security interceptor from our open API definition file. We add this extension as a dependency for the Maven plugin `org.openapitools:openapi-generator-maven-plugin`.

```xml
<plugin>
    <groupId>org.openapitools</groupId>
    <artifactId>openapi-generator-maven-plugin</artifactId>
    <configuration>
        <additionalProperties>onecx-scopes=true</additionalProperties>
        <!-- configuration -->
    </configuration>
    <executions><!-- executions --></executions>
    <dependencies>
        <dependency>
            <groupId>org.tkit.onecx.quarkus</groupId>
            <artifactId>onecx-openapi-generator</artifactId>
        </dependency>
    </dependencies>
</plugin>
```

To enable this extension, we also need to define additional properties `onecx-scopes=true`. Without this configuration, the generator uses the default Java source code template.

Now our generated source code contains the annotation `@io.quarkus.security.PermissionsAllowed({"read"})` to the generated method.

```java
public interface RoleInternalApi {

    @io.quarkus.security.PermissionsAllowed({ "read" })
    @GET
    @Consumes({ "application/json" })
    @Produces({ "application/json" })
    Response createRole();

}
```

The `org.tkit.onecx.quarkus:onecx-security` extension creates security audit data for the default Quarkus security extension during the build process. After enabling this extension, it is no longer possible to call this method without a token and with the scope `read`.

| |  To disable security setup following property tkit.security.auth.enabled=false. This property is part fo (tkit-quarkus-url)\[1000kit Quarkus extension\] |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#%5Fsecurity%5Ftests)Security tests

For testing we use Quarkus `Keycloak` dev services. To activate this feature add this maven dependency.

```xml
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-test-keycloak-server</artifactId>
    <scope>test</scope>
</dependency>
```

Quarkus will start and configure a `Keycloak` server for our tests but also in the dev mode by default. Now we can configure `user` and they `roles`. For example, we add role `role-admin` to user `alice` in our example

```properties
# Enabled security for all requests /* and exclude /q/* quarkus console
quarkus.http.auth.permission.health.paths=/q/*
quarkus.http.auth.permission.health.policy=permit
quarkus.http.auth.permission.default.paths=/*
quarkus.http.auth.permission.default.policy=authenticated

# TEST
%test.quarkus.keycloak.devservices.roles.alice=role-admin
%test.quarkus.keycloak.devservices.roles.bob=role-user

# DEV
%dev.quarkus.keycloak.devservices.roles.alice=role-admin
%dev.quarkus.keycloak.devservices.roles.bob=role-user
```

| |  How to import the whole realm or configure additional user in to Keycloak dev services please check the [Quarkus documentation](https://quarkus.io/guides/) page. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Now we can use the `io.quarkus.test.keycloak.client.KeycloakTestClient` in our test.

Example test class 

```java
@QuarkusTest
@TestHTTPEndpoint(RoleRestController.class)
class RoleRestControllerTest {

    // create keycloak client instance connected to keycloak dev service container
    KeycloakTestClient keycloakClient = new KeycloakTestClient();

     @Test
    void oauthTest() {
         // get the access token of the user alice
        var token = keycloakClient.getAccessToken("alice");

        // call rest endpoint
        given().when()
                .auth().oauth2(token)
                .contentType(APPLICATION_JSON).get("1").then()
                .statusCode(Response.Status.OK.getStatusCode());

        // test without oauth token
        given().when().contentType(APPLICATION_JSON).get("1").then()
                .statusCode(Response.Status.UNAUTHORIZED.getStatusCode());
    }
}
```

### [](#%5Fmulti%5Ftenancy)Multi tenancy

For multi tenancy we will to use [onecx-quarkus-tenant](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/index.html) extension.

| |  For more information about the configuration please check the documentation page [onecx-quarkus-tenant](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/index.html) |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Multi tenancy maven dependencies 

```xml
<dependencies>
        <!-- ONECX -->
        <dependency>
            <groupId>org.tkit.onecx.quarkus</groupId>
            <artifactId>onecx-tenant</artifactId>
        </dependency>
        <!-- 1000kit -->
        <dependency>
            <groupId>org.tkit.quarkus.lib</groupId>
            <artifactId>tkit-quarkus-jpa</artifactId>
        </dependency>
</dependencies>
```

Now we need to configure our application

```properties
# hibernate multi-tenant configuration
quarkus.hibernate-orm.multitenant=DISCRIMINATOR

# enable or disable multi-tenancy support
tkit.rs.context.tenant-id.enabled=true
```

| |  Header configuration for the token, and token parsing is implemented in 1000kit [tkit-rest-context](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/index.html) quarkus extensions. Please check the documentation of the extension. |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#%5Fmulti%5Ftenancy%5Ftests)Multi tenancy tests

For the test we can use mock settings where we can define which claim attribute of the token we will use: `%test.tkit.rs.context.tenant-id.mock.claim-org-id=orgId` and we must define mapping between token claim value and tenant ID `%test.tkit.rs.context.tenant-id.mock.data.<claim-value>=<tenant-id>`.

```properties
%test.tkit.rs.context.tenant-id.enabled=true
%test.tkit.rs.context.tenant-id.mock.enabled=true
%test.tkit.rs.context.tenant-id.mock.default-tenant=default
%test.tkit.rs.context.tenant-id.mock.claim-org-id=orgId
%test.tkit.rs.context.tenant-id.mock.data.org1=tenant-100
%test.tkit.rs.context.tenant-id.mock.data.org2=tenant-200
```

For the test we can create a simple help method which will creates a token for our tests

```java
@SuppressWarnings("java:S2187")
public class AbstractTest {

    // header ID of the principal token for tests
    protected static final String APM_HEADER_PARAM = "apm-principal-token";

    // token claim for tenant-id
    protected static final String CLAIMS_ORG_ID = ConfigProvider.getConfig()
            .getValue("%test.tkit.rs.context.tenant-id.mock.claim-org-id", String.class);

   /**
    * Method creates a principal token for test.
    * @param organizationId organization ID
    * @return the corresponding test
    */
    protected static String createToken(String organizationId) {
        try {
            String userName = "test-user";
            JsonObjectBuilder claims = Json.createObjectBuilder();
            claims.add(Claims.preferred_username.name(), userName);
            claims.add(Claims.sub.name(), userName);
            claims.add(CLAIMS_ORG_ID, organizationId);
            PrivateKey privateKey = KeyUtils.generateKeyPair(2048).getPrivate();
            return Jwt.claims(claims.build()).sign(privateKey);
        } catch (Exception ex) {
            throw new RuntimeException(ex);
        }
    }
}
```

In our test we can use `createToken` method to create a token

```java
@QuarkusTest
@TestHTTPEndpoint(ExampleRestController.class)
class ExampleRestControllerTenantTest extends AbstractTest {

    @Test
    void createNewThemeTest() {
        var dto = given()
                .when()
                .contentType(APPLICATION_JSON)
                .header(APM_HEADER_PARAM, createToken("org1"))
                .body(themeDto)
                .post()
                .then()
                .statusCode(CREATED.getStatusCode())
                .extract()
                .body().as(ExampleDTO.class);
    }
}
```
