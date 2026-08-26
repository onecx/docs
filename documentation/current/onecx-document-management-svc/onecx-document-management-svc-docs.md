# undefined

[Link to Docker registry](https://github.com/onecx/onecx-document-management-svc/pkgs/container/onecx-document-management-svc)

## [](#%5Fdefault%5Fproperties)Default properties

src/main/resources/application.properties 

```properties
quarkus.http.auth.permission.health.paths=/q/*
quarkus.http.auth.permission.health.policy=permit
quarkus.http.auth.permission.default.paths=/*
quarkus.http.auth.permission.default.policy=authenticated
quarkus.banner.enabled=false
quarkus.http.limits.max-body-size=20240K
quarkus.liquibase.migrate-at-start=true
tkit.security-dynamic-test.openapi.enabled=false
quarkus.datasource.db-kind=postgresql
quarkus.datasource.jdbc.max-size=8
quarkus.datasource.jdbc.min-size=2
quarkus.datasource.metrics.enabled=true
quarkus.hibernate-orm.metrics.enabled=true
quarkus.hibernate-orm.database.generation=none
quarkus.hibernate-orm.database.generation.halt-on-error=true
quarkus.hibernate-orm.jdbc.timezone=UTC
quarkus.log.category."org.hibernate.engine.internal.StatisticalLoggingSessionEventListener".level=WARNING
tkit.log.json.enabled=true
tkit.log.json.keys.type=rs-time=double,time=double,rs-response-status=int
tkit.log.json.keys.mdc=traceId=X-B3-TraceId,spanId=X-B3-SpanId
tkit.log.json.keys.ignore=loggerClassName,ndc
tkit.log.json.keys.override=timestamp=@timestamp,threadName=thread,loggerName=source
tkit.log.json.keys.env=service_domain=SERVICE_DOMAIN
quarkus.jacoco.excludes=**/mappers/*
## TEST
```

## [](#%5Fextensions)Extensions

Extensions List 

| Extensions                             | Documentation                                                                                  | Configuration                                                                                                                                    | Version |
| -------------------------------------- | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------- |
| tkit-quarkus-log-rs                    | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-rs.html)   | [Link](https://github.com/1000kit/tkit-quarkus/blob/4.6.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-rs.adoc)                     | 4.6.0   |
| tkit-quarkus-log-cdi                   | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-cdi.html)  | [Link](https://github.com/1000kit/tkit-quarkus/blob/4.6.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-cdi.adoc)                    | 4.6.0   |
| tkit-quarkus-log-json                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-json.html) | [Link](https://github.com/1000kit/tkit-quarkus/blob/4.6.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-json.adoc)                   | 4.6.0   |
| tkit-quarkus-jpa                       | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-jpa.html)      | [Link](https://github.com/1000kit/tkit-quarkus/blob/4.6.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-jpa.adoc)                        | 4.6.0   |
| tkit-quarkus-rest                      | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/4.6.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest.adoc)                       | 4.6.0   |
| quarkus-rest                           | [Link](https://quarkus.io/guides/rest)                                                         | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest.adoc)                           | 3.27.1  |
| quarkus-rest-jackson                   | [Link](https://quarkus.io/guides/rest-json)                                                    | 3.27.1                                                                                                                                           |         |
| quarkus-arc                            | [Link](https://quarkus.io/guides/cdi-reference)                                                | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-arc.adoc)                            | 3.27.1  |
| quarkus-smallrye-openapi               | [Link](https://quarkus.io/guides/openapi-swaggerui)                                            | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-openapi.adoc)               | 3.27.1  |
| quarkus-liquibase                      | [Link](https://quarkus.io/guides/liquibase)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-liquibase.adoc)                      | 3.27.1  |
| quarkus-jdbc-postgresql                | [Link](https://quarkus.io/guides/datasource)                                                   | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-jdbc-postgresql.adoc)                | 3.27.1  |
| quarkus-hibernate-validator            | [Link](https://quarkus.io/guides/validation)                                                   | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-hibernate-validator.adoc)            | 3.27.1  |
| quarkus-smallrye-jwt                   | [Link](https://quarkus.io/guides/security-jwt-build)                                           | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-jwt.adoc)                   | 3.27.1  |
| quarkus-smallrye-health                | [Link](https://quarkus.io/guides/smallrye-health)                                              | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-health.adoc)                | 3.27.1  |
| quarkus-oidc                           | [Link](https://quarkus.io/guides/security-oidc-bearer-token-authentication-tutorial)           | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-oidc.adoc)                           | 3.27.1  |
| tkit-quarkus-security                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-security.html) | [Link](https://github.com/1000kit/tkit-quarkus/blob/4.6.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-security.adoc)                   | 4.6.0   |
| onecx-core                             | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-core.html)       | 2.3.0                                                                                                                                            |         |
| quarkus-micrometer-registry-prometheus | [Link](https://quarkus.io/guides/telemetry-micrometer)                                         | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-micrometer-registry-prometheus.adoc) | 3.27.1  |
| quarkus-opentelemetry                  | [Link](https://quarkus.io/guides/opentelemetry)                                                | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-opentelemetry.adoc)                  | 3.27.1  |
| quarkus-container-image-docker         | [Link](https://quarkus.io/guides/container-image)                                              | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-container-image-docker.adoc)         | 3.27.1  |
| quarkus-scheduler                      | 3.27.1                                                                                         |                                                                                                                                                  |         |

## [](#%5Fhelm)Helm

[Link to Helm registry](https://github.com/onecx/onecx-document-management-svc/pkgs/container/charts%2Fonecx-document-management-svc)

Default values in src/main/helm/values.yaml

```yaml
app:
  image:
    repository: "onecx-apps/onecx-document-management-svc"
  db:
    enabled: true
  product: false
```
