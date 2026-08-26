# undefined

## [](#%5Fonecx%5Fopenapi%5Fgenerator)onecx-openapi-generator

### [](#%5Finstallation)Installation

```xml
<plugin>
    <groupId>org.openapitools</groupId>
    <artifactId>openapi-generator-maven-plugin</artifactId>
    <version>${openapitools.openapi-generator-maven-plugin.version}</version>
    <dependencies>
        <dependency>
            <groupId>org.tkit.onecx.quarkus</groupId>
            <artifactId>onecx-openapi-generator</artifactId>
            <version>3.0.0</version>
        </dependency>
    </dependencies>
</plugin>
```

### [](#%5Fconfiguration)Configuration

#### [](#%5Foauth2%5Fscopes)OAuth2 scopes

To enable the OpenAPI generator extension for OAuth2 scopes from the OpenAPI definition file, use the following additional property `onecx-scopes=true` in the maven plugin configuration.

```xml
<plugin>
    <groupId>org.openapitools</groupId>
    <artifactId>openapi-generator-maven-plugin</artifactId>
    <configuration>
        <!-- configuration -->
        <additionalProperties>onecx-scopes=true</additionalProperties>
        <configOptions>
            <!-- configuration options -->
        </configOptions>
    </configuration>
</plugin>
```

Define OAuth2 scopes in your openapi file.

```yaml
openapi: 3.0.3
info:
  title: example
  version: 1.0.0
servers:
  - url: "http://localhost:8080"
paths:
  /v1/themes:
    get:
      security:
        - oauth2: [ ocx-th:read ]
      operationId: getThemesInfo
      responses:
        200:
          description: OK
components:
  securitySchemes:
    oauth2:
      type: oauth2
      flows:
        clientCredentials:
          tokenUrl: https://oauth.simple.api/token
          scopes:
            ocx-th:read: Grants read access
```

The generated Java source code contains the additional Quarkus annotation `io.quarkus.security.PermissionsAllowed` with the scope defined in the OpenAPI file.

```java
    @io.quarkus.security.PermissionsAllowed({ "ocx-th:read" })
    @GET
    @Produces({ "application/json" })
    Response getThemesInfo();
```

#### [](#%5Fpermissions)Permissions

To enable the OpenAPI generator extension for OneCX permissions from the OpenAPI definition file, use the following additional property `onecx-permissions=true` in the maven plugin configuration.

```xml
<plugin>
    <groupId>org.openapitools</groupId>
    <artifactId>openapi-generator-maven-plugin</artifactId>
    <configuration>
        <!-- configuration -->
        <additionalProperties>onecx-scopes=true</additionalProperties>
        <configOptions>
            <!-- configuration options -->
        </configOptions>
    </configuration>
</plugin>
```

Define Onecx permission in your openapi file as vendor extension.

```yaml
   x-onecx:
    permissions:
     themes:
      - read
```

Openapi example:

```yaml
openapi: 3.0.3
info:
  title: example
  version: 1.0.0
servers:
  - url: "http://localhost:8080"
paths:
 /themes:
  get:
   x-onecx:
    permissions:
     themes:
      - read
   operationId: getThemes
   responses:
    200:
     description: OK
```

The generated Java source code contains the additional Quarkus annotation `io.quarkus.security.PermissionsAllowed` with the scope defined in the OpenAPI file.

```java
    @io.quarkus.security.PermissionsAllowed({ "onecx:themes#read" })
    @GET
    @Produces({ "application/json" })
    Response getThemes();
```

#### [](#%5Fconstraints)Constraints

To enable the OpenAPI generator extension for OneCX validator from the OpenAPI definition file, use the following additional property `onecx-constraints=true` in the maven plugin configuration.

| |  This feature requires the extension [onecx-validator](onecx-validator.html) in the classpath |
| ----------------------------------------------------------------------------------------------- |

```xml
<plugin>
    <groupId>org.openapitools</groupId>
    <artifactId>openapi-generator-maven-plugin</artifactId>
    <configuration>
        <!-- configuration -->
        <additionalProperties>onecx-constraints=true</additionalProperties>
        <configOptions>
            <!-- configuration options -->
        </configOptions>
    </configuration>
</plugin>
```

Define Onecx constraints in your openapi file as vendor extension.

```yaml
   x-onecx:
    constraints:
     size:
        min: 10
        max: 100
        key: paramKey
```

Openapi example:

```yaml
openapi: 3.0.3
info:
  title: example
  version: 1.0.0
servers:
  - url: "http://localhost:8080"
paths:
 /themes:
  post:
   operationId: createThemes
   parameters:
     - in: header
       name: Content-Length
       required: true
       x-onecx:
         constraints:
           size:
             min: 10
             max: 100
             key: paramKey
   responses:
    200:
     description: OK
```

The generated Java source code contains the additional Quarkus annotation `org.tkit.onecx.quarkus.validator.constraints.Size` with the size constraints defined in the OpenAPI file.

```java
    @HeaderParam("Content-Length") @NotNull
    @org.tkit.onecx.quarkus.validator.constraints.Size(
            min = 10,
            max = 100,
            key = "paramKey")
```
