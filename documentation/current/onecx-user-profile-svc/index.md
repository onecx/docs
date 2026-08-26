# OneCX User Profile Backend Service

## [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                                      | Type   | Default       |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ------------- |
| [onecx.user-profile.claims.display-name](#onecx-user-profile-svc%5Fonecx-user-profile-claims-display-name) User profile display name token claim Environment variable: ONECX\_USER\_PROFILE\_CLAIMS\_DISPLAY\_NAME          | string | name          |
| [onecx.user-profile.claims.email](#onecx-user-profile-svc%5Fonecx-user-profile-claims-email) User profile email token claim Environment variable: ONECX\_USER\_PROFILE\_CLAIMS\_EMAIL                                       | string | email         |
| [onecx.user-profile.claims.first-name](#onecx-user-profile-svc%5Fonecx-user-profile-claims-first-name) User profile first name token claim Environment variable: ONECX\_USER\_PROFILE\_CLAIMS\_FIRST\_NAME                  | string | given\_name   |
| [onecx.user-profile.claims.last-name](#onecx-user-profile-svc%5Fonecx-user-profile-claims-last-name) User profile last name token claim Environment variable: ONECX\_USER\_PROFILE\_CLAIMS\_LAST\_NAME                      | string | family\_name  |
| [onecx.user-profile.claims.organization-id](#onecx-user-profile-svc%5Fonecx-user-profile-claims-organization-id) User profile organization token claim Environment variable: ONECX\_USER\_PROFILE\_CLAIMS\_ORGANIZATION\_ID | string | orgId         |
| [onecx.user-profile.claims.locale](#onecx-user-profile-svc%5Fonecx-user-profile-claims-locale) User profile locale Environment variable: ONECX\_USER\_PROFILE\_CLAIMS\_LOCALE                                               | string |               |
| [onecx.user-profile.claims.timezone](#onecx-user-profile-svc%5Fonecx-user-profile-claims-timezone) User profile timezone Environment variable: ONECX\_USER\_PROFILE\_CLAIMS\_TIMEZONE                                       | string |               |
| [onecx.user-profile.claims.menu-mode](#onecx-user-profile-svc%5Fonecx-user-profile-claims-menu-mode) User profile menu Environment variable: ONECX\_USER\_PROFILE\_CLAIMS\_MENU\_MODE                                       | string |               |
| [onecx.user-profile.settings.locale](#onecx-user-profile-svc%5Fonecx-user-profile-settings-locale) User profile locale Environment variable: ONECX\_USER\_PROFILE\_SETTINGS\_LOCALE                                         | string | en            |
| [onecx.user-profile.settings.timezone](#onecx-user-profile-svc%5Fonecx-user-profile-settings-timezone) User profile timezone Environment variable: ONECX\_USER\_PROFILE\_SETTINGS\_TIMEZONE                                 | string | Europe/Berlin |
| [onecx.user-profile.settings.menu-mode](#onecx-user-profile-svc%5Fonecx-user-profile-settings-menu-mode) User profile menu Environment variable: ONECX\_USER\_PROFILE\_SETTINGS\_MENU\_MODE                                 | string | STATIC        |

[Link to Docker registry](https://github.com/onecx/onecx-user-profile-svc/pkgs/container/onecx-user-profile-svc)

## [](#%5Fdefault%5Fproperties)Default properties

src/main/resources/application.properties 

```properties
quarkus.datasource.db-kind=postgresql
quarkus.datasource.jdbc.max-size=30
quarkus.datasource.jdbc.min-size=10
quarkus.datasource.metrics.enabled=true
quarkus.banner.enabled=false
quarkus.hibernate-orm.database.generation=validate
quarkus.hibernate-orm.multitenant=DISCRIMINATOR
quarkus.hibernate-orm.jdbc.timezone=UTC
quarkus.hibernate-orm.metrics.enabled=true
quarkus.liquibase.migrate-at-start=true
quarkus.liquibase.validate-on-migrate=true
quarkus.http.auth.permission.health.paths=/q/*
quarkus.http.auth.permission.health.policy=permit
quarkus.http.auth.permission.default.paths=/*
quarkus.http.auth.permission.default.policy=authenticated
tkit.rs.context.tenant-id.enabled=true
%prod.quarkus.oidc-client.client-id=${quarkus.application.name}
%prod.quarkus.datasource.jdbc.url=${DB_URL:jdbc:postgresql://postgresdb:5432/onecx-user-profile?sslmode=disable}
%prod.quarkus.datasource.username=${DB_USER:onecx-user-profile}
%prod.quarkus.datasource.password=${DB_PWD:onecx-user-profile}
```

## [](#%5Fextensions)Extensions

Extensions List 

| Extensions                             | Documentation                                                                                      | Configuration                                                                                                                                    | Version |
| -------------------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------- |
| tkit-quarkus-jpa                       | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-jpa.html)          | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-jpa.adoc)                        | 5.1.0   |
| tkit-quarkus-log-cdi                   | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-cdi.html)      | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-cdi.adoc)                    | 5.1.0   |
| tkit-quarkus-log-rs                    | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-rs.html)       | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-rs.adoc)                     | 5.1.0   |
| tkit-quarkus-log-json                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-json.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-json.adoc)                   | 5.1.0   |
| tkit-quarkus-rest                      | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest.html)         | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest.adoc)                       | 5.1.0   |
| onecx-tenant                           | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-tenant.html)         | [Link](https://github.com/onecx/onecx-quarkus/blob/3.0.0/docs/modules/onecx-quarkus/pages/includes/onecx-tenant.adoc)                            | 3.0.0   |
| tkit-quarkus-jpa-tenant                | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-jpa-tenant.html)   | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-jpa-tenant.adoc)                 | 5.1.0   |
| tkit-quarkus-rest-context              | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest-context.html) | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest-context.adoc)               | 5.1.0   |
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
| onecx-core                             | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-core.html)           | 3.0.0                                                                                                                                            |         |
| quarkus-container-image-docker         | [Link](https://quarkus.io/guides/container-image)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-container-image-docker.adoc)         | 3.33.1  |

## [](#%5Fhelm)Helm

[Link to Helm registry](https://github.com/onecx/onecx-user-profile-svc/pkgs/container/charts%2Fonecx-user-profile-svc)

Default values in src/main/helm/values.yaml

```yaml
app:
  name: svc
  image:
    repository: "onecx/onecx-user-profile-svc"
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
        description: OneCX User Profile Backend Service
        name: OneCX User Profile SVC
```
