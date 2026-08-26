# OneCX Identity Access Management Backend Service

## [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                          | Type   | Default  |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- |
| [onecx.iam.keycloaks."keycloaks".display-name](#onecx-iam-svc%5Fonecx-iam-keycloaks-keycloaks-display-name) Display name for keycloak Environment variable: ONECX\_IAM\_KEYCLOAKS\_\_KEYCLOAKS\_\_DISPLAY\_NAME | string | required |
| [onecx.iam.keycloaks."keycloaks".description](#onecx-iam-svc%5Fonecx-iam-keycloaks-keycloaks-description) Description for keycloak Environment variable: ONECX\_IAM\_KEYCLOAKS\_\_KEYCLOAKS\_\_DESCRIPTION      | string |          |
| [onecx.iam.keycloaks."keycloaks".url](#onecx-iam-svc%5Fonecx-iam-keycloaks-keycloaks-url) url of keycloak Environment variable: ONECX\_IAM\_KEYCLOAKS\_\_KEYCLOAKS\_\_URL                                       | string | required |
| [onecx.iam.keycloaks."keycloaks".issuerHost](#onecx-iam-svc%5Fonecx-iam-keycloaks-keycloaks-issuerhost) Baseurl of keycloak Environment variable: ONECX\_IAM\_KEYCLOAKS\_\_KEYCLOAKS\_\_ISSUERHOST              | string | required |
| [onecx.iam.keycloaks."keycloaks".realm](#onecx-iam-svc%5Fonecx-iam-keycloaks-keycloaks-realm) Keycloak realm Environment variable: ONECX\_IAM\_KEYCLOAKS\_\_KEYCLOAKS\_\_REALM                                  | string | required |
| [onecx.iam.keycloaks."keycloaks".client](#onecx-iam-svc%5Fonecx-iam-keycloaks-keycloaks-client) Client for keylcloak admin api Environment variable: ONECX\_IAM\_KEYCLOAKS\_\_KEYCLOAKS\_\_CLIENT               | string | required |
| [onecx.iam.keycloaks."keycloaks".secret](#onecx-iam-svc%5Fonecx-iam-keycloaks-keycloaks-secret) Client secret Environment variable: ONECX\_IAM\_KEYCLOAKS\_\_KEYCLOAKS\_\_SECRET                                | string | required |
| [onecx.iam.keycloaks."keycloaks".username](#onecx-iam-svc%5Fonecx-iam-keycloaks-keycloaks-username) Username for keycloak admin api access Environment variable: ONECX\_IAM\_KEYCLOAKS\_\_KEYCLOAKS\_\_USERNAME | string | required |
| [onecx.iam.keycloaks."keycloaks".password](#onecx-iam-svc%5Fonecx-iam-keycloaks-keycloaks-password) User password Environment variable: ONECX\_IAM\_KEYCLOAKS\_\_KEYCLOAKS\_\_PASSWORD                          | string | required |

[Link to Docker registry](https://github.com/onecx/onecx-iam-svc/pkgs/container/onecx-iam-svc)

## [](#%5Fdefault%5Fproperties)Default properties

src/main/resources/application.properties 

```properties
quarkus.keycloak.admin-client.server-url=http://keycloak:8080
quarkus.keycloak.admin-client.realm=master
quarkus.keycloak.admin-client.username=admin
quarkus.keycloak.admin-client.password=admin
quarkus.http.auth.permission.health.paths=/q/*
quarkus.http.auth.permission.health.policy=permit
quarkus.http.auth.permission.default.paths=/*
quarkus.http.auth.permission.default.policy=authenticated
quarkus.http.test-port=0
keycloak.cors=true
```

## [](#%5Fextensions)Extensions

Extensions List 

| Extensions                             | Documentation                                                                                      | Configuration                                                                                                                                    | Version |
| -------------------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------- |
| tkit-quarkus-log-cdi                   | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-cdi.html)      | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-cdi.adoc)                    | 5.1.0   |
| tkit-quarkus-log-rs                    | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-rs.html)       | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-rs.adoc)                     | 5.1.0   |
| tkit-quarkus-log-json                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-json.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-json.adoc)                   | 5.1.0   |
| tkit-quarkus-rest                      | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest.html)         | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest.adoc)                       | 5.1.0   |
| tkit-quarkus-rest-context              | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest-context.html) | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest-context.adoc)               | 5.1.0   |
| quarkus-opentelemetry                  | [Link](https://quarkus.io/guides/opentelemetry)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-opentelemetry.adoc)                  | 3.33.1  |
| quarkus-smallrye-health                | [Link](https://quarkus.io/guides/smallrye-health)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-health.adoc)                | 3.33.1  |
| quarkus-micrometer-registry-prometheus | [Link](https://quarkus.io/guides/telemetry-micrometer)                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-micrometer-registry-prometheus.adoc) | 3.33.1  |
| quarkus-rest                           | [Link](https://quarkus.io/guides/rest)                                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest.adoc)                           | 3.33.1  |
| quarkus-rest-jackson                   | [Link](https://quarkus.io/guides/rest-json)                                                        | 3.33.1                                                                                                                                           |         |
| quarkus-smallrye-openapi               | [Link](https://quarkus.io/guides/openapi-swaggerui)                                                | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-openapi.adoc)               | 3.33.1  |
| quarkus-smallrye-jwt                   | [Link](https://quarkus.io/guides/security-jwt-build)                                               | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-jwt.adoc)                   | 3.33.1  |
| quarkus-hibernate-validator            | [Link](https://quarkus.io/guides/validation)                                                       | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-hibernate-validator.adoc)            | 3.33.1  |
| quarkus-oidc                           | [Link](https://quarkus.io/guides/security-oidc-bearer-token-authentication-tutorial)               | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-oidc.adoc)                           | 3.33.1  |
| tkit-quarkus-security                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-security.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-security.adoc)                   | 5.1.0   |
| onecx-core                             | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-core.html)           | 3.0.0                                                                                                                                            |         |
| quarkus-arc                            | [Link](https://quarkus.io/guides/cdi-reference)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-arc.adoc)                            | 3.33.1  |
| quarkus-container-image-docker         | [Link](https://quarkus.io/guides/container-image)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-container-image-docker.adoc)         | 3.33.1  |
| quarkus-keycloak-admin-rest-client     | 3.33.1                                                                                             |                                                                                                                                                  |         |

## [](#%5Fhelm)Helm

[Link to Helm registry](https://github.com/onecx/onecx-iam-svc/pkgs/container/charts%2Fonecx-iam-svc)

Default values in src/main/helm/values.yaml

```yaml
app:
  name: svc
  image:
    repository: "onecx/onecx-iam-svc"
  db:
    enabled: false
```
