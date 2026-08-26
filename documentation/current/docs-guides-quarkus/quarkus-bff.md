# Backend for Frontends (BFF) with Quarkus

A backend for frontend (BFF) is a specialized backend service that serves the needs of a specific frontend application or user interface.  
It acts as an intermediary layer between the frontend and various backend services, aggregating data and handling business logic tailored to the requirements of the frontend.

## [](#%5Fproject%5Fsetup)Project setup

Now that [project structure](project-structure.html) is set up for the Onecx Quarkus project, we can configure the backend for frontends and extend the project configuration.

### [](#%5Fparent%5Fconfiguration)Parent configuration

Project maven parent configuration, artifactId and project version.

| |  More information about maven parent pom pattern [Apache Maven Pom Documentation](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html) |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Maven parent configuration 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>org.tkit.onecx</groupId>
        <artifactId>onecx-quarkus3-parent</artifactId>
        <version>0.62.0</version>
    </parent>

    <artifactId>onecx-example-svc</artifactId>
    <version>999-SNAPSHOT</version>

</project>
```

### [](#%5Fdependencies)Dependencies

Include all needed dependencies. Depending on your project they may vary but the following will fit for most cases.

Dependencies 

```xml
<dependencies>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-rest</artifactId>
    </dependency>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-smallrye-openapi</artifactId>
    </dependency>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-rest-jackson</artifactId>
    </dependency>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-smallrye-health</artifactId>
    </dependency>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-opentelemetry</artifactId>
    </dependency>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-micrometer-registry-prometheus</artifactId>
    </dependency>
    <dependency>
        <groupId>io.quarkiverse.openapi.generator</groupId>
        <artifactId>quarkus-openapi-generator</artifactId>
    </dependency>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-rest-client-jackson</artifactId>
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
    <dependency>
        <groupId>org.tkit.quarkus.lib</groupId>
        <artifactId>tkit-quarkus-rest-context</artifactId>
    </dependency>
    <dependency>
        <groupId>org.mapstruct</groupId>
        <artifactId>mapstruct</artifactId>
    </dependency>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-hibernate-validator</artifactId>
    </dependency>
    <dependency>
        <groupId>org.tkit.onecx.quarkus</groupId>
        <artifactId>onecx-permissions</artifactId>
    </dependency>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-oidc</artifactId>
    </dependency>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-rest-client-oidc-filter</artifactId>
    </dependency>
    <dependency>
        <groupId>org.tkit.quarkus.lib</groupId>
        <artifactId>tkit-quarkus-security</artifactId>
    </dependency>
    <!-- DEV -->
    <dependency>
        <groupId>io.quarkiverse.mockserver</groupId>
        <artifactId>quarkus-mockserver</artifactId>
        <scope>provided</scope>
    </dependency>

    <!-- TEST -->
    <dependency>
        <groupId>io.quarkiverse.mockserver</groupId>
        <artifactId>quarkus-mockserver-test</artifactId>
        <exclusions>
            <exclusion>
                <groupId>io.swagger.parser.v3</groupId>
                <artifactId>swagger-parser</artifactId>
            </exclusion>
        </exclusions>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>io.swagger.parser.v3</groupId>
        <artifactId>swagger-parser</artifactId>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-test-keycloak-server</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

### [](#%5Fapplication%5Fproperties)application.properties

Add the following properties. They may vary depending on your project. This is just a base set.

application.properties 

```xml
# AUTHENTICATION
quarkus.http.auth.permission.health.paths=/q/*
quarkus.http.auth.permission.health.policy=permit
quarkus.http.auth.permission.default.paths=/*
quarkus.http.auth.permission.default.policy=authenticated
onecx.permissions.application-id=${quarkus.application.name}


# propagate the apm-principal-token from requests we receive
org.eclipse.microprofile.rest.client.propagateHeaders=apm-principal-token
# OIDC
%prod.quarkus.oidc-client.client-id=${quarkus.application.name}

# INTEGRATION TEST
quarkus.test.integration-test-profile=test
# TEST
%test.quarkus.http.test-port=0
%test.tkit.log.json.enabled=false
%test.quarkus.mockserver.devservices.config-class-path=true
%test.quarkus.mockserver.devservices.config-file=/mockserver.properties
%test.quarkus.mockserver.devservices.config-dir=/mockserver
%test.quarkus.mockserver.devservices.log=false
%test.quarkus.mockserver.devservices.reuse=true

%test.tkit.rs.context.token.header-param=apm-principal-token
%test.tkit.rs.context.token.enabled=false
%test.tkit.rs.context.tenant-id.mock.claim-org-id=orgId
%test.quarkus.rest-client.onecx_permission.url=${quarkus.mockserver.endpoint}
%test.quarkus.keycloak.devservices.roles.alice=role-admin
%test.quarkus.keycloak.devservices.roles.bob=role-user
%test.quarkus.oidc-client.auth-server-url=${quarkus.oidc.auth-server-url}
%test.quarkus.oidc-client.client-id=${quarkus.oidc.client-id}
%test.quarkus.oidc-client.credentials.secret=${quarkus.oidc.credentials.secret}
%test.onecx.permissions.product-name=applications
# PIPE CONFIG
```

### [](#%5Fopenapi%5Fgenerator)OpenApi generator

After creating your OpenAPI file in the right [ directory ](project-structure.html) :

Maven pom configuration for BFF-Api ⇒ Code 

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.openapitools</groupId>
            <artifactId>openapi-generator-maven-plugin</artifactId>
            <executions>
                <execution>
                    <id>internal</id>
                    <goals>
                        <goal>generate</goal>
                    </goals>
                    <configuration>
                        <inputSpec>src/main/openapi/openapi-bff.yaml</inputSpec>
                        <apiPackage>gen.org.tkit.onecx.your-product-name.bff.rs.internal</apiPackage>
                        <modelPackage>gen.org.tkit.onecx.your-product-name.bff.rs.internal.model</modelPackage>
                        <typeMappings>File=byte[]</typeMappings>
                    </configuration>
                </execution>
            </executions>
            <configuration>
                <additionalProperties>onecx-permissions=true</additionalProperties>
                <generatorName>jaxrs-spec</generatorName>
                <apiNameSuffix>ApiService</apiNameSuffix>
                <modelNameSuffix>DTO</modelNameSuffix>
                <generateApiTests>false</generateApiTests>
                <generateApiDocumentation>false</generateApiDocumentation>
                <generateModelTests>false</generateModelTests>
                <generateModelDocumentation>false</generateModelDocumentation>
                <generateSupportingFiles>false</generateSupportingFiles>
                <addCompileSourceRoot>true</addCompileSourceRoot>
                <library>quarkus</library>
                <configOptions>
                    <sourceFolder>/</sourceFolder>
                    <openApiNullable>false</openApiNullable>
                    <returnResponse>true</returnResponse>
                    <useTags>true</useTags>
                    <interfaceOnly>true</interfaceOnly>
                    <serializableModel>true</serializableModel>
                    <singleContentTypes>false</singleContentTypes>
                    <dateLibrary>java8</dateLibrary>
                    <useMicroProfileOpenAPIAnnotations>true</useMicroProfileOpenAPIAnnotations>
                    <useJakartaEe>true</useJakartaEe>
                    <useSwaggerAnnotations>false</useSwaggerAnnotations>
                    <java17>true</java17>
                </configOptions>
            </configuration>
        </plugin>
    </plugins>
</build>
```

Maven pom configuration for client-api download 

```xml
<plugin>
    <groupId>com.googlecode.maven-download-plugin</groupId>
    <artifactId>download-maven-plugin</artifactId>
    <executions>
        <execution>
            <id>add-a-unique-and-describing-id-here</id>
            <phase>generate-resources</phase>
            <goals>
                <goal>wget</goal>
            </goals>
            <configuration>
                <url>
                    add your github raw url here
                </url>
                <outputDirectory>target/tmp/openapi</outputDirectory>
                <outputFileName>your-output-file-name.yaml</outputFileName>
                <skipCache>true</skipCache>
            </configuration>
        </execution>
    </executions>
</plugin>
```

application.properties for code-generation 

```xml
quarkus.openapi-generator.codegen.input-base-dir=target/tmp/openapi

# your client
quarkus.openapi-generator.codegen.spec.your-output-file-name.config-key=yourCustomConfigKey
quarkus.openapi-generator.codegen.spec.your-output-file-name.base-package=gen.org.tkit.onecx.yourProductName.client
quarkus.openapi-generator.codegen.spec.your-output-file-name.return-response=true
quarkus.openapi-generator.codegen.spec.your-output-file-name.additional-api-type-annotations=@org.eclipse.microprofile.rest.client.annotation.RegisterClientHeaders;
quarkus.openapi-generator.codegen.spec.your-output-file-name.additional-model-type-annotations=@io.quarkus.runtime.annotations.RegisterForReflection;
quarkus.openapi-generator.codegen.spec.your-output-file-name.enable-security-generation=false
%prod.quarkus.rest-client.yourCustomConfigKey.providers=io.quarkus.oidc.client.reactive.filter.OidcClientRequestReactiveFilter
%test.quarkus.rest-client.yourCustomConfigKey.providers=io.quarkus.oidc.client.reactive.filter.OidcClientRequestReactiveFilter

%prod.quarkus.rest-client.yourCustomConfigKey.url=http://url-of-the-client:8080
%test.quarkus.rest-client.yourCustomConfigKey.url=${quarkus.mockserver.endpoint}
```

| |  The download of a clients openapi file only works for non-secured open-source files. Otherwise you need to manually paste the openapi file into your project and adjust your application.properties. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#%5Fcreating%5Fa%5Frest%5Fcontroller)Creating a Rest-Controller

After writing your openapi file run `mvn clean package` or `mvn clean package -DskipTests`to generate objects and your rest-controller interface into the /target folder.

Controller definition and annotations 

```java
@ApplicationScoped
@Transactional(value = Transactional.TxType.NOT_SUPPORTED)
@LogService
public class ThemeRestController implements ThemesApiService {
```

Use of client and mapper 

```java
    @Inject
    @RestClient
    ThemesInternalApi client;

    @Inject
    ThemeMapper mapper;

    @Inject
    ExceptionMapper exceptionMapper;
```

Endpoint implementation 

```yaml
  /themes/search:
    post:
      x-onecx:
        permissions:
          themes:
            - read
      tags:
        - themes
      description: Search themes by criteria
      operationId: searchThemes
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ThemeSearchCriteria'
      responses:
        "200":
          description: Ok
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ThemePageResult'
        "204":
          description: No Content
        "400":
          description: Bad Request
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProblemDetailResponse'
        "404":
          description: Not Found
```

```java
    @Override
    public Response searchThemes(ThemeSearchCriteriaDTO themeSearchCriteriaDTO) {
        try (Response response = client.searchThemes(mapper.mapSearchCriteria(themeSearchCriteriaDTO))) {
            ThemePageResultDTO themePageResultDTO = mapper
                    .pageResultMapper(response.readEntity(ThemePageResult.class));
            return Response.status(response.getStatus()).entity(themePageResultDTO).build();
        }
    }
```

Exception handling 

In most cases you don’t need to handle exceptions manually. We define **@ServerExceptionMapper**to let quarkus automatically handle the mentioned exceptions. For this to work you need to use a custom ExceptionMapper so that the Exceptions will be converted to an equal format. You can just use the following file.

```java
package org.tkit.onecx.themes.bff.rs.mappers;

import static jakarta.ws.rs.core.MediaType.APPLICATION_JSON;

import java.util.List;
import java.util.Map;
import java.util.Set;

import gen.org.tkit.onecx.theme.bff.rs.internal.model.ProblemDetailInvalidParamDTO;
import gen.org.tkit.onecx.theme.bff.rs.internal.model.ProblemDetailParamDTO;
import gen.org.tkit.onecx.theme.bff.rs.internal.model.ProblemDetailResponseDTO;
import jakarta.validation.ConstraintViolation;
import jakarta.validation.ConstraintViolationException;
import jakarta.validation.Path;
import jakarta.ws.rs.core.Response;

import org.jboss.resteasy.reactive.ClientWebApplicationException;
import org.jboss.resteasy.reactive.RestResponse;
import org.mapstruct.Mapper;
import org.mapstruct.Mapping;
import org.tkit.quarkus.rs.mappers.OffsetDateTimeMapper;

import gen.org.tkit.onecx.permission.model.ProblemDetailResponse;

@Mapper(uses = { OffsetDateTimeMapper.class })
public interface ExceptionMapper {

    default RestResponse<ProblemDetailResponseDTO> constraint(ConstraintViolationException ex) {
        var dto = exception("CONSTRAINT_VIOLATIONS", ex.getMessage());
        dto.setInvalidParams(createErrorValidationResponse(ex.getConstraintViolations()));
        return RestResponse.status(Response.Status.BAD_REQUEST, dto);
    }

    default Response clientException(ClientWebApplicationException ex) {
        if (ex.getResponse().getStatus() == 500) {
            return Response.status(400).build();
        } else {
            if (ex.getResponse().getMediaType() != null
                    && ex.getResponse().getMediaType().toString().contains(APPLICATION_JSON)) {
                return Response.status(ex.getResponse().getStatus())
                        .entity(map(ex.getResponse().readEntity(ProblemDetailResponse.class))).build();
            } else {
                return Response.status(ex.getResponse().getStatus()).build();
            }
        }
    }

    @Mapping(target = "removeParamsItem", ignore = true)
    @Mapping(target = "removeInvalidParamsItem", ignore = true)
    ProblemDetailResponseDTO map(ProblemDetailResponse problemDetailResponse);

    @Mapping(target = "removeParamsItem", ignore = true)
    @Mapping(target = "params", ignore = true)
    @Mapping(target = "invalidParams", ignore = true)
    @Mapping(target = "removeInvalidParamsItem", ignore = true)
    ProblemDetailResponseDTO exception(String errorCode, String detail);

    default List<ProblemDetailParamDTO> map(Map<String, Object> params) {
        if (params == null) {
            return List.of();
        }
        return params.entrySet().stream().map(e -> {
            var item = new ProblemDetailParamDTO();
            item.setKey(e.getKey());
            if (e.getValue() != null) {
                item.setValue(e.getValue().toString());
            }
            return item;
        }).toList();
    }

    List<ProblemDetailInvalidParamDTO> createErrorValidationResponse(
            Set<ConstraintViolation<?>> constraintViolation);

    @Mapping(target = "name", source = "propertyPath")
    @Mapping(target = "message", source = "message")
    ProblemDetailInvalidParamDTO createError(ConstraintViolation<?> constraintViolation);

    default String mapPath(Path path) {
        return path.toString();
    }
}
```

After this you can add the following to your rest-controller.

```java
    @ServerExceptionMapper
    public RestResponse<ProblemDetailResponseDTO> constraint(ConstraintViolationException ex) {
        return exceptionMapper.constraint(ex);
    }

    @ServerExceptionMapper
    public Response restException(ClientWebApplicationException ex) {
        return exceptionMapper.clientException(ex);
    }
```

| |  Depending on your project, you may have more or less exceptions that need to be handled. When using multiple clients in one rest-call it’s also possible, that you need to manually handle exceptions with a **catch{}** block. |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#%5Fmapper)Mapper

Create a mapper for each entity. We use Mapstruct for this.[Mapstruct Documentation](https://mapstruct.org/documentation/stable/reference/html/)

You need to map all incoming dto’s to the svc models and the model of the svc response back to a dto.

Mapper Example 

Mapper

```java
@Mapper(uses = { OffsetDateTimeMapper.class })
public interface ThemeMapper {

    ThemeSearchCriteria mapSearchCriteria(ThemeSearchCriteriaDTO themeSearchCriteriaDTO);

    @Mapping(target = "themes", source = "stream")
    @Mapping(target = "removeThemesItem", ignore = true)
    ThemePageResultDTO pageResultMapper(ThemePageResult themePageResult);
}
```

Used in controller

```java
@Override
public Response searchThemes(ThemeSearchCriteriaDTO themeSearchCriteriaDTO) {
    try (Response response = client.searchThemes(mapper.mapSearchCriteria(themeSearchCriteriaDTO))) {
        ThemePageResultDTO themePageResultDTO = mapper
                .pageResultMapper(response.readEntity(ThemePageResult.class));
        return Response.status(response.getStatus()).entity(themePageResultDTO).build();
    }
}
```

### [](#%5Flogger)Logger

Since your controller is already annotated with `@LogService`You can now create a custom logger. You should add each incoming object to the logger but only as little as possible and as much as necessary fields for each object.

Logger Example 

```java
@ApplicationScoped
public class ThemeLog implements LogParam {
    @Override
    public List<Item> getClasses() {
        return List.of(
                this.item(10, ThemeSearchCriteriaDTO.class,
                        x -> "ThemeSearchCriteriaDTO[ name: " +
                                ((ThemeSearchCriteriaDTO) x).getName()
                                + " ]"));
    }
}
```

| |  Make sure that you don’t add critical data to logger like passwords or tokens! |
| --------------------------------------------------------------------------------- |

## [](#%5Ftests)Tests

To start writing unit-tests you should first create an abstract class called `AbstractTest.java` inside of your test package. You can copy and paste the following class.

AbstractTest.java 

```java
package org.tkit.onecx.themes.bff.rs;

import org.eclipse.microprofile.config.ConfigProvider;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;
import com.fasterxml.jackson.datatype.jsr310.JavaTimeModule;

import io.quarkiverse.mockserver.test.MockServerTestResource;
import io.quarkus.test.common.QuarkusTestResource;
import io.restassured.RestAssured;
import io.restassured.config.ObjectMapperConfig;
import io.restassured.config.RestAssuredConfig;

@QuarkusTestResource(MockServerTestResource.class)
public abstract class AbstractTest {
    protected static final String ADMIN = "alice";

    protected static final String USER = "bob";

    protected static final String APM_HEADER_PARAM = ConfigProvider.getConfig()
            .getValue("%test.tkit.rs.context.token.header-param", String.class);

    static {
        RestAssured.config = RestAssuredConfig.config().objectMapperConfig(
                ObjectMapperConfig.objectMapperConfig().jackson2ObjectMapperFactory(
                        (cls, charset) -> {
                            ObjectMapper objectMapper = new ObjectMapper();
                            objectMapper.registerModule(new JavaTimeModule());
                            objectMapper.configure(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS, false);
                            return objectMapper;
                        }));
    }
}
```

We use the `@QuarkusTestResource(MockServerTestResource.class)` annotation to include a mockserver for our tests.

The following defined users `bob` and `alice` are later used to test the access with different sets of permissions.`Alice` is used as an admin with all permissions and `bob` as a user with just a subset of permissions. The `APM_HEADER_PARAM` is later used to authenticate our test requests. See more at [Security & Permissions](#%5Fsecurity%5Fpermissions)

Whenever your data contains any type of dates you will also need the static RestAssured.config Otherwise the test responses will contain dates as numbers.

### [](#%5Fmockserver)Mockserver

Now, before writing tests, we will add all necessary files to make the mockserver work.

1. Create a package called `mockserver` inside your test resources package. See [project structure](project-structure.html) for more information.
2. Create an empty file called `internal.json` in this package. This file will be used by the mockserver to save expectations whenever you create one inside your tests.
3. Create a file called `mockserver.properties` inside your test.resources package. You can copy and paste the content from the following file:  
mockserver.properties  
```yaml  
mockserver.initializationJsonPath=/mockserver/*.json  
# watch changes in the file  
mockserver.watchInitializationJson=true  
# Certificate Generation  
# dynamically generated CA key pair (if they don't already exist in specified directory)  
mockserver.dynamicallyCreateCertificateAuthorityCertificate=true  
# save dynamically generated CA key pair in working directory  
mockserver.directoryToSaveDynamicSSLCertificate=.  
# certificate domain name (default "localhost")  
mockserver.sslCertificateDomainName=localhost  
# comma separated list of ip addresses for Subject Alternative Name domain names (default empty list)  
mockserver.sslSubjectAlternativeNameDomains=www.example.com,www.another.com  
# comma separated list of ip addresses for Subject Alternative Name ips (default empty list)  
mockserver.sslSubjectAlternativeNameIps=127.0.0.1  
```
4. Add the following properties to your application.properties  
application.properties  
```yaml  
%test.quarkus.mockserver.devservices.config-class-path=true  
%test.quarkus.mockserver.devservices.config-file=/mockserver.properties  
%test.quarkus.mockserver.devservices.config-dir=/mockserver  
%test.quarkus.mockserver.devservices.log=false  
%test.quarkus.mockserver.devservices.reuse=true  
%test.quarkus.rest-client.onecx_theme_svc.url=${quarkus.mockserver.endpoint}  
```

You will need to change the last line from `onecx_theme_svc` to the config key of your client. This will point all test requests to your client to the mockserver.

You will need this line for each client you use.

### [](#%5Funit%5Ftests)Unit Tests

Now everything is prepared to write your first test. Each rest-controller class will have its own test class. First create a new test class. By convention, you should name it like this:`[RestControllerName]Test`.

Define your class

```java
@QuarkusTest
@LogService
@TestHTTPEndpoint(ThemeRestController.class)
class ThemeRestControllerTest extends AbstractTest {
```

The `@TestHTTPEndpoint` will set the base-url of your test-request to the one of your controller.

Mapper Example 

If you have a bff with 6 endpoints distributed to 2 controllers like:

```text
/yourBff/themes/{id} (GET)
/yourBff/themes (POST)
/yourBff/themes/search (POST)
/yourBff/users/{id} (GET)
/yourBff/users (POST)
/yourBff/users/search (POST)
```

This would result in 2 controllers. One for themes and one for users. When testing the ThemesRestController you can now make test-request to just`.post(/search)`, `.post(/{id})`, `.post()` because the base URL of your tests will already include "/yourBff/themes".

Now instantiate a `KeycloakTestClient` and inject the `MockServerClient`:

```java
    KeycloakTestClient keycloakClient = new KeycloakTestClient();

    @InjectMockServerClient
    MockServerClient mockServerClient;
```

Now you should also add the following `@BeforeEach` method to reset all mocks after each test. Since you probably want to run multiple test cases related to a single client-endpoint, this method ensures, that you don’t hit a created expectation of a before executed test by accident.

```java
    static final String MOCK_ID = "MOCK";

    @BeforeEach
    void resetExpectation() {
        try {
            mockServerClient.clear(MOCK_ID);
        } catch (Exception ex) {
            //  mockId not existing
        }
    }
```

| |  You can also manually remove a created expectation in a test itself. If you need to mock multiple endpoints in a single test, you can add more mock ids to the resetExpectation() method. Make sure, that in a single test all mocks have a unique id. Otherwise, they would overwrite themselves. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

The following example test will test a POST "/search" endpoint.

For a unit test you need to create a method annotated with `@Test`

| |  Tests should have a describing name including the expectation. For example searchThemesByCriteria() or searchThemes\_missingCriteria\_400() |
| ---------------------------------------------------------------------------------------------------------------------------------------------- |

A test needs three main components:

Expectation (Mock)

```java
        mockServerClient.when(request().withPath("/internal/themes/search").withMethod(HttpMethod.POST)
                .withBody(JsonBody.json(criteria)))
                .withId(MOCK_ID)
                .respond(httpRequest -> response().withStatusCode(Response.Status.OK.getStatusCode())
                        .withContentType(MediaType.APPLICATION_JSON)
                        .withBody(JsonBody.json(data)));
```

Request

```java
        var output = given()
                .when()
                .auth().oauth2(keycloakClient.getAccessToken(ADMIN))
                .header(APM_HEADER_PARAM, ADMIN)
                .contentType(APPLICATION_JSON)
                .body(searchThemeRequestDTO)
                .post()
                .then()
                .statusCode(Response.Status.OK.getStatusCode())
                .contentType(APPLICATION_JSON)
                .extract().as(ThemePageResultDTO.class);
```

Assertions

```java
        Assertions.assertNotNull(output);
        Assertions.assertEquals(data.getSize(), output.getSize());
        Assertions.assertEquals(data.getStream().size(), output.getThemes().size());
        Assertions.assertEquals(data.getStream().get(0).getName(), output.getThemes().get(0).getName());
```

See more in [GitHub Theme BFF reference](https://github.com/onecx/onecx-theme-bff/blob/main/src/test/java/org/tkit/onecx/themes/bff/rs/ThemeRestControllerTest.java) for an example test class.

### [](#%5Fintegration%5Ftests%5Fit)Integration Tests (IT)

ITs ensure that everything also works when your application is containerized with docker. Create for each test class an integration test file named like:`[RestControllerName]IT`. Annotate this class with `@QuarkusIntegrationTest` and extend it by your test class.

It should look like this

```java
@QuarkusIntegrationTest
public class ThemeRestControllerIT extends ThemeRestControllerTest {
}
```

## [](#%5Fsecurity%5Fpermissions)Security & Permissions

Our BFFs are double secured. To activate endpoint security you need to add the following properties to the application.

properties

```yaml
# AUTHENTICATION
quarkus.http.auth.permission.health.paths=/q/*
quarkus.http.auth.permission.health.policy=permit
quarkus.http.auth.permission.default.paths=/*
quarkus.http.auth.permission.default.policy=authenticated
```

This will ensure, that the BFF is only accessible for requests with a valid APM token. All requests in your test file will then need  
`.header(APM_HEADER_PARAM, ADMIN)`  
which we already added before.

To limit access based on permissions first make sure you added the following dependency to your pom.

pom: OneCX Permissions dependency

```xml
        
            org.tkit.onecx.quarkus
            onecx-permissions
        
```

and activated the permission generation of the `openapi-generator-maven-plugin`.

pom: OneCX Permissions generation

```xml
                    onecx-permissions=true
```

After that you can add permissions to each endpoint inside your openapi file.

openapi.yaml

```yaml
  /themes/search:
    post:
      x-onecx:
        permissions:
          themes:
            - read
```

We typically use `read`, `write` and `delete` as actions.  
This may vary depending on the project. Each permission is a pair of resource(entity) + action. In this example case the resource(entity) is "themes" and the action "read".

After that you need to add those permissions to the values.yaml.

values.yaml

```yaml
app:
 name: bff
 image:
  repository: "onecx/onecx-theme-bff"
 operator:
  # Permission
  permission:
   enabled: true
   spec:
    permissions:
     themes:
      read: permission on all GET requests and POST search
      write: permission on PUT, POST, PATCH requests, where objects are saved or updated
      delete: permission on all DELETE requests
  keycloak:
   client:
    enabled: true
    spec:
     kcConfig:
      defaultClientScopes: [ ocx-th:all, ocx-pm:read ]
```

This will trigger an operator on each deployment which creates those permissions in the permission-svc.

To use those permissions in your tests you firstly need to add the following to each request.`.auth().oauth2(keycloakClient.getAccessToken(ADMIN))`

and this to your application.properties

application.properties

```yaml
%test.quarkus.rest-client.onecx_permission.url=${quarkus.mockserver.endpoint}
%test.quarkus.keycloak.devservices.roles.alice=role-admin
%test.quarkus.keycloak.devservices.roles.bob=role-user
%test.onecx.permissions.product-name=applications
```

Finally, we need to add mocks for the permission-svc. You can copy and paste the content of the following file and save it into the mockserver folder as permissions.json and adjust it by changing the resource, in this case "themes", and actions if needed.

permissions.json 

```json
[
  {
    "id": "2",
    "httpRequest": {
      "headers": {
        "apm-principal-token": [
          "alice"
        ]
      },
      "path": "/v1/permissions/user/applications/onecx-theme-bff"
    },
    "httpResponse": {
      "body": {
        "type": "JSON",
        "json": {
          "appId": "onecx-theme-bff",
          "permissions": {
            "themes": [
              "read",
              "write",
              "delete"
            ],
            "permissions": [
              "admin-write",
              "admin-read"
            ]
          }
        },
        "contentType": "application/json"
      }
    }
  },
  {
    "id": "3",
    "httpRequest": {
      "headers": {
        "apm-principal-token": [
          "bob"
        ]
      },
      "path": "/v1/permissions/user/applications/onecx-theme-bff"
    },
    "httpResponse": {
      "body": {
        "type": "JSON",
        "json": {
          "appId": "onecx-theme-bff",
          "permissions": {
            "themes": [
              "read"
            ],
            "permissions": [
              "admin-write",
              "admin-read"
            ]
          }
        },
        "contentType": "application/json"
      }
    }
  }
]
```
