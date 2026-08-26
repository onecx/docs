# OneCX Bookmark Backend Service

## [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                            | Type    | Default                  |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ------------------------ |
| [onecx.bookmark.default.enabled](#onecx-bookmark-svc%5Fonecx-bookmark-default-enabled) Enable or disable default bookmark Environment variable: ONECX\_BOOKMARK\_DEFAULT\_ENABLED | boolean | false                    |
| [onecx.bookmark.default.url](#onecx-bookmark-svc%5Fonecx-bookmark-default-url) Default bookmark URL Environment variable: ONECX\_BOOKMARK\_DEFAULT\_URL                           | string  | https://github.com/onecx |
| [onecx.bookmark.product-item-id](#onecx-bookmark-svc%5Fonecx-bookmark-product-item-id) Default bookmark URL Environment variable: ONECX\_BOOKMARK\_PRODUCT\_ITEM\_ID              | string  | PRODUCT\_BASE\_DOC\_URL  |

[Link to Docker registry](https://github.com/onecx/onecx-bookmark-svc/pkgs/container/onecx-bookmark-svc)

## [](#%5Fdefault%5Fproperties)Default properties

src/main/resources/application.properties 

```properties
quarkus.datasource.db-kind=postgresql
quarkus.datasource.jdbc.max-size=30
quarkus.datasource.jdbc.min-size=10
quarkus.datasource.metrics.enabled=true
quarkus.http.auth.permission.health.paths=/q/*
quarkus.http.auth.permission.health.policy=permit
quarkus.http.auth.permission.default.paths=/*
quarkus.http.auth.permission.default.policy=authenticated
quarkus.hibernate-orm.database.generation=validate
quarkus.hibernate-orm.multitenant=DISCRIMINATOR
quarkus.hibernate-orm.jdbc.timezone=UTC
quarkus.hibernate-orm.metrics.enabled=true
quarkus.hibernate-orm.mapping.format.global=ignore
quarkus.liquibase.migrate-at-start=true
quarkus.liquibase.validate-on-migrate=true
tkit.dataimport.enabled=false
tkit.dataimport.configurations.template.file=import/template.json
tkit.dataimport.configurations.template.metadata.tenants=default
tkit.dataimport.configurations.template.class-path=true
tkit.dataimport.configurations.template.enabled=false
tkit.dataimport.configurations.template.stop-at-error=true
tkit.rs.context.tenant-id.enabled=true
%prod.quarkus.oidc-client.client-id=${quarkus.application.name}
%prod.quarkus.datasource.jdbc.url=${DB_URL:jdbc:postgresql://postgresdb:5432/onecx-bookmark?sslmode=disable}
%prod.quarkus.datasource.username=${DB_USER:onecx-bookmark}
%prod.quarkus.datasource.password=${DB_PWD:onecx-bookmark}
onecx.validator.values.mapping.bookmark-image-size=bookmark-image-size
onecx.parameters.product-name=onecx-bookmark
```

## [](#%5Fextensions)Extensions

Extensions List 

| Extensions                             | Documentation                                                                                      | Configuration                                                                                                                                    | Version  |
| -------------------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| onecx-core                             | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-core.html)           | 3.0.0                                                                                                                                            |          |
| onecx-tenant                           | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-tenant.html)         | [Link](https://github.com/onecx/onecx-quarkus/blob/3.0.0/docs/modules/onecx-quarkus/pages/includes/onecx-tenant.adoc)                            | 3.0.0    |
| quarkus-oidc                           | [Link](https://quarkus.io/guides/security-oidc-bearer-token-authentication-tutorial)               | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-oidc.adoc)                           | 3.33.1.1 |
| tkit-quarkus-rest-context              | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest-context.html) | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest-context.adoc)               | 5.1.0    |
| tkit-quarkus-jpa-tenant                | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-jpa-tenant.html)   | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-jpa-tenant.adoc)                 | 5.1.0    |
| tkit-quarkus-data-import               | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-data-import.html)  | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-data-import.adoc)                | 5.1.0    |
| tkit-quarkus-jpa                       | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-jpa.html)          | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-jpa.adoc)                        | 5.1.0    |
| tkit-quarkus-log-cdi                   | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-cdi.html)      | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-cdi.adoc)                    | 5.1.0    |
| tkit-quarkus-log-rs                    | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-rs.html)       | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-rs.adoc)                     | 5.1.0    |
| tkit-quarkus-log-json                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-json.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-json.adoc)                   | 5.1.0    |
| tkit-quarkus-rest                      | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest.html)         | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest.adoc)                       | 5.1.0    |
| quarkus-arc                            | [Link](https://quarkus.io/guides/cdi-reference)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-arc.adoc)                            | 3.33.1.1 |
| quarkus-liquibase                      | [Link](https://quarkus.io/guides/liquibase)                                                        | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-liquibase.adoc)                      | 3.33.1.1 |
| quarkus-smallrye-health                | [Link](https://quarkus.io/guides/smallrye-health)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-health.adoc)                | 3.33.1.1 |
| quarkus-micrometer-registry-prometheus | [Link](https://quarkus.io/guides/telemetry-micrometer)                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-micrometer-registry-prometheus.adoc) | 3.33.1.1 |
| quarkus-hibernate-orm                  | [Link](https://quarkus.io/guides/hibernate-orm)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-hibernate-orm.adoc)                  | 3.33.1.1 |
| quarkus-rest                           | [Link](https://quarkus.io/guides/rest)                                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest.adoc)                           | 3.33.1.1 |
| quarkus-rest-jackson                   | [Link](https://quarkus.io/guides/rest-json)                                                        | 3.33.1.1                                                                                                                                         |          |
| quarkus-jdbc-postgresql                | [Link](https://quarkus.io/guides/datasource)                                                       | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-jdbc-postgresql.adoc)                | 3.33.1.1 |
| quarkus-smallrye-openapi               | [Link](https://quarkus.io/guides/openapi-swaggerui)                                                | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-openapi.adoc)               | 3.33.1.1 |
| quarkus-hibernate-validator            | [Link](https://quarkus.io/guides/validation)                                                       | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-hibernate-validator.adoc)            | 3.33.1.1 |
| quarkus-opentelemetry                  | [Link](https://quarkus.io/guides/opentelemetry)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-opentelemetry.adoc)                  | 3.33.1.1 |
| onecx-parameters                       | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-parameters.html)     | [Link](https://github.com/onecx/onecx-quarkus/blob/3.0.0/docs/modules/onecx-quarkus/pages/includes/onecx-parameters.adoc)                        | 3.0.0    |
| tkit-quarkus-security                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-security.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-security.adoc)                   | 5.1.0    |
| quarkus-container-image-docker         | [Link](https://quarkus.io/guides/container-image)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-container-image-docker.adoc)         | 3.33.1.1 |
| quarkus-smallrye-context-propagation   | 3.33.1.1                                                                                           |                                                                                                                                                  |          |
| onecx-validator                        | 3.0.0                                                                                              |                                                                                                                                                  |          |

## [](#%5Fhelm)Helm

[Link to Helm registry](https://github.com/onecx/onecx-bookmark-svc/pkgs/container/charts%2Fonecx-bookmark-svc)

Default values in src/main/helm/values.yaml

```yaml
app:
  name: svc
  image:
    repository: "onecx/onecx-bookmark-svc"
  db:
    enabled: true
  operator:
    keycloak:
      client:
        enabled: true
        spec:
          kcConfig:
            defaultClientScopes: [ ocx-tn:read, ocx-pa-ap:read, ocx-pa-me:write ]
    microservice:
      spec:
        description: OneCX Bookmark Backend Service
        name: OneCX Bookmark SVC
    parameter:
      enabled: true
      spec:
        parameters:
          default:
            bookmark-image-size:
              displayName: Bookmark Image Size Parameter
              description:
              value:
                min: 1
                max: 110000
                message: Image Size Constraint Violation
```
