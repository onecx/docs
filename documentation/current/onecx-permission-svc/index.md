# OneCX Permission Backend Service

## [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                                                                                   | Type               | Default                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------ | ------------------------------ |
| [onecx.permission.token.verified](#onecx-permission-svc%5Fonecx-permission-token-verified) Verified permission token Environment variable: ONECX\_PERMISSION\_TOKEN\_VERIFIED                                                                                            | boolean            | false                          |
| [onecx.permission.token.issuer.public-key-location.suffix](#onecx-permission-svc%5Fonecx-permission-token-issuer-public-key-location-suffix) Issuer public key location suffix. Environment variable: ONECX\_PERMISSION\_TOKEN\_ISSUER\_PUBLIC\_KEY\_LOCATION\_SUFFIX    | string             | /protocol/openid-connect/certs |
| [onecx.permission.token.issuer.public-key-location.enabled](#onecx-permission-svc%5Fonecx-permission-token-issuer-public-key-location-enabled) Issuer public key location enabled Environment variable: ONECX\_PERMISSION\_TOKEN\_ISSUER\_PUBLIC\_KEY\_LOCATION\_ENABLED | boolean            | false                          |
| [onecx.permission.token.claim.separator](#onecx-permission-svc%5Fonecx-permission-token-claim-separator) Claim separator Environment variable: ONECX\_PERMISSION\_TOKEN\_CLAIM\_SEPARATOR                                                                                | string             |                                |
| [onecx.permission.token.claim.path](#onecx-permission-svc%5Fonecx-permission-token-claim-path) Claim path Environment variable: ONECX\_PERMISSION\_TOKEN\_CLAIM\_PATH                                                                                                    | string             | realm\_access/roles            |
| [onecx.permission.default-roles](#onecx-permission-svc%5Fonecx-permission-default-roles) Add default roles to the user token Environment variable: ONECX\_PERMISSION\_DEFAULT\_ROLES                                                                                     | list of string     |                                |
| [onecx.permission.template.role-mapping."role-mapping"](#onecx-permission-svc%5Fonecx-permission-template-role-mapping-role-mapping) Role mapping for the template import Environment variable: ONECX\_PERMISSION\_TEMPLATE\_ROLE\_MAPPING\_\_ROLE\_MAPPING\_            | Map<String,String> |                                |
| [onecx.permission.template.tenants](#onecx-permission-svc%5Fonecx-permission-template-tenants) Template import tenants Environment variable: ONECX\_PERMISSION\_TEMPLATE\_TENANTS                                                                                        | list of string     | default                        |

[Link to Docker registry](https://github.com/onecx/onecx-permission-svc/pkgs/container/onecx-permission-svc)

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
quarkus.native.resources.includes=import/template.json
quarkus.hibernate-orm.database.generation=validate
quarkus.hibernate-orm.multitenant=DISCRIMINATOR
quarkus.hibernate-orm.jdbc.timezone=UTC
quarkus.hibernate-orm.metrics.enabled=true
quarkus.liquibase.migrate-at-start=true
quarkus.liquibase.validate-on-migrate=true
tkit.rs.context.tenant-id.enabled=true
onecx.permission.token.verified=true
onecx.permission.token.issuer.public-key-location.suffix=/protocol/openid-connect/certs
onecx.permission.token.issuer.public-key-location.enabled=false
onecx.permission.token.claim.path=realm_access/roles
tkit.dataimport.enabled=false
tkit.dataimport.configurations.template.file=import/template.json
tkit.dataimport.configurations.template.class-path=true
tkit.dataimport.configurations.template.enabled=false
tkit.dataimport.configurations.template.stop-at-error=true
%prod.quarkus.datasource.jdbc.url=${DB_URL:jdbc:postgresql://postgresdb:5432/onecx-permission?sslmode=disable}
%prod.quarkus.datasource.username=${DB_USER:onecx-permission}
%prod.quarkus.datasource.password=${DB_PWD:onecx-permission}
%prod.quarkus.oidc-client.client-id=${quarkus.application.name}
```

## [](#%5Fextensions)Extensions

Extensions List 

| Extensions                             | Documentation                                                                                      | Configuration                                                                                                                                    | Version |
| -------------------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------- |
| onecx-core                             | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-core.html)           | 3.0.0                                                                                                                                            |         |
| onecx-tenant                           | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-tenant.html)         | [Link](https://github.com/onecx/onecx-quarkus/blob/3.0.0/docs/modules/onecx-quarkus/pages/includes/onecx-tenant.adoc)                            | 3.0.0   |
| tkit-quarkus-data-import               | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-data-import.html)  | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-data-import.adoc)                | 5.1.0   |
| tkit-quarkus-rest-context              | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest-context.html) | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest-context.adoc)               | 5.1.0   |
| tkit-quarkus-jpa-tenant                | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-jpa-tenant.html)   | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-jpa-tenant.adoc)                 | 5.1.0   |
| tkit-quarkus-jpa                       | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-jpa.html)          | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-jpa.adoc)                        | 5.1.0   |
| tkit-quarkus-log-cdi                   | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-cdi.html)      | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-cdi.adoc)                    | 5.1.0   |
| tkit-quarkus-log-rs                    | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-rs.html)       | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-rs.adoc)                     | 5.1.0   |
| tkit-quarkus-log-json                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-json.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-json.adoc)                   | 5.1.0   |
| tkit-quarkus-rest                      | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest.html)         | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest.adoc)                       | 5.1.0   |
| quarkus-arc                            | [Link](https://quarkus.io/guides/cdi-reference)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-arc.adoc)                            | 3.33.1  |
| quarkus-liquibase                      | [Link](https://quarkus.io/guides/liquibase)                                                        | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-liquibase.adoc)                      | 3.33.1  |
| quarkus-smallrye-health                | [Link](https://quarkus.io/guides/smallrye-health)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-health.adoc)                | 3.33.1  |
| quarkus-micrometer-registry-prometheus | [Link](https://quarkus.io/guides/telemetry-micrometer)                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-micrometer-registry-prometheus.adoc) | 3.33.1  |
| quarkus-hibernate-orm                  | [Link](https://quarkus.io/guides/hibernate-orm)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-hibernate-orm.adoc)                  | 3.33.1  |
| quarkus-rest                           | [Link](https://quarkus.io/guides/rest)                                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest.adoc)                           | 3.33.1  |
| quarkus-rest-jackson                   | [Link](https://quarkus.io/guides/rest-json)                                                        | 3.33.1                                                                                                                                           |         |
| quarkus-jdbc-postgresql                | [Link](https://quarkus.io/guides/datasource)                                                       | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-jdbc-postgresql.adoc)                | 3.33.1  |
| quarkus-smallrye-openapi               | [Link](https://quarkus.io/guides/openapi-swaggerui)                                                | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-openapi.adoc)               | 3.33.1  |
| quarkus-hibernate-validator            | [Link](https://quarkus.io/guides/validation)                                                       | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-hibernate-validator.adoc)            | 3.33.1  |
| quarkus-opentelemetry                  | [Link](https://quarkus.io/guides/opentelemetry)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-opentelemetry.adoc)                  | 3.33.1  |
| quarkus-oidc                           | [Link](https://quarkus.io/guides/security-oidc-bearer-token-authentication-tutorial)               | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-oidc.adoc)                           | 3.33.1  |
| tkit-quarkus-security                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-security.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-security.adoc)                   | 5.1.0   |
| quarkus-container-image-docker         | [Link](https://quarkus.io/guides/container-image)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-container-image-docker.adoc)         | 3.33.1  |
| quarkus-smallrye-context-propagation   | 3.33.1                                                                                             |                                                                                                                                                  |         |

## [](#%5Fhelm)Helm

[Link to Helm registry](https://github.com/onecx/onecx-permission-svc/pkgs/container/charts%2Fonecx-permission-svc)

Default values in src/main/helm/values.yaml

```yaml
app:
  name: svc
  image:
    repository: "onecx/onecx-permission-svc"
  db:
    enabled: true
  operator:
    keycloak:
      client:
        enabled: true
        spec:
          kcConfig:
            defaultClientScopes: [ ocx-tn:read ]
    microservice:
      spec:
        description: OneCX Permission Backend Service
        name: OneCX Permission SVC
```
