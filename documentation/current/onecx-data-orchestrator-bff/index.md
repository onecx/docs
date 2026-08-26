# OneCX Data Orchestrator Backend For Frontend

## [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                                                       | Type    | Default  |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- |
| [onecx.data.orchestrator.types."types".enabled](#onecx-data-orchestrator-bff%5Fonecx-data-orchestrator-types-types-enabled) Enable or disable a specific resource Environment variable: ONECX\_DATA\_ORCHESTRATOR\_TYPES\_\_TYPES\_\_ENABLED | boolean | true     |
| [onecx.data.orchestrator.types."types".value](#onecx-data-orchestrator-bff%5Fonecx-data-orchestrator-types-types-value) Kind value from custom resource definition Environment variable: ONECX\_DATA\_ORCHESTRATOR\_TYPES\_\_TYPES\_\_VALUE  | string  | required |

[Link to Docker registry](https://github.com/onecx/onecx-data-orchestrator-bff/pkgs/container/onecx-data-orchestrator-bff)

## [](#%5Fdefault%5Fproperties)Default properties

src/main/resources/application.properties 

```properties
quarkus.http.auth.permission.health.paths=/q/*
quarkus.http.auth.permission.health.policy=permit
quarkus.http.auth.permission.default.paths=/*
quarkus.http.auth.permission.default.policy=authenticated
onecx.permissions.application-id=${quarkus.application.name}
onecx.permissions.product-name=onecx-data-orchestrator
quarkus.kubernetes-client.trust-certs=true
%prod.quarkus.oidc-client.client-id=${quarkus.application.name}
onecx.data.orchestrator.types.data.enabled=true
onecx.data.orchestrator.types.data.value=Data
onecx.data.orchestrator.types.database.enabled=true
onecx.data.orchestrator.types.database.value=Database
onecx.data.orchestrator.types.keycloak-client.enabled=true
onecx.data.orchestrator.types.keycloak-client.value=KeycloakClient
onecx.data.orchestrator.types.microfrontend.enabled=true
onecx.data.orchestrator.types.microfrontend.value=Microfrontend
onecx.data.orchestrator.types.microservice.enabled=true
onecx.data.orchestrator.types.microservice.value=Microservice
onecx.data.orchestrator.types.parameter.enabled=true
onecx.data.orchestrator.types.parameter.value=Parameter
onecx.data.orchestrator.types.permission.enabled=true
onecx.data.orchestrator.types.permission.value=Permission
onecx.data.orchestrator.types.product.enabled=true
onecx.data.orchestrator.types.product.value=Product
onecx.data.orchestrator.types.slot.enabled=true
onecx.data.orchestrator.types.slot.value=Slot
```

## [](#%5Fextensions)Extensions

Extensions List 

| Extensions                             | Documentation                                                                                      | Configuration                                                                                                                                    | Version    |
| -------------------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- |
| quarkus-rest                           | [Link](https://quarkus.io/guides/rest)                                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest.adoc)                           | 3.33.1     |
| quarkus-smallrye-openapi               | [Link](https://quarkus.io/guides/openapi-swaggerui)                                                | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-openapi.adoc)               | 3.33.1     |
| quarkus-rest-jackson                   | [Link](https://quarkus.io/guides/rest-json)                                                        | 3.33.1                                                                                                                                           |            |
| quarkus-smallrye-health                | [Link](https://quarkus.io/guides/smallrye-health)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-health.adoc)                | 3.33.1     |
| quarkus-opentelemetry                  | [Link](https://quarkus.io/guides/opentelemetry)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-opentelemetry.adoc)                  | 3.33.1     |
| quarkus-micrometer-registry-prometheus | [Link](https://quarkus.io/guides/telemetry-micrometer)                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-micrometer-registry-prometheus.adoc) | 3.33.1     |
| quarkus-openapi-generator              | [Link](https://docs.quarkiverse.io/quarkus-openapi-generator/dev/index.html)                       | [Link](https://github.com/quarkiverse/quarkus-openapi-generator/blob/2.16.0-lts/docs/modules/ROOT/pages/includes/quarkus-openapi-generator.adoc) | 2.16.0-lts |
| quarkus-rest-client-jackson            | [Link](https://quarkus.io/guides/rest-client)                                                      | 3.33.1                                                                                                                                           |            |
| tkit-quarkus-log-cdi                   | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-cdi.html)      | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-cdi.adoc)                    | 5.1.0      |
| tkit-quarkus-log-rs                    | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-rs.html)       | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-rs.adoc)                     | 5.1.0      |
| tkit-quarkus-log-json                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-json.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-json.adoc)                   | 5.1.0      |
| tkit-quarkus-rest                      | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest.html)         | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest.adoc)                       | 5.1.0      |
| tkit-quarkus-rest-context              | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest-context.html) | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest-context.adoc)               | 5.1.0      |
| quarkus-hibernate-validator            | [Link](https://quarkus.io/guides/validation)                                                       | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-hibernate-validator.adoc)            | 3.33.1     |
| onecx-permissions                      | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-permissions.html)    | [Link](https://github.com/onecx/onecx-quarkus/blob/3.0.0/docs/modules/onecx-quarkus/pages/includes/onecx-permissions.adoc)                       | 3.0.0      |
| quarkus-oidc                           | [Link](https://quarkus.io/guides/security-oidc-bearer-token-authentication-tutorial)               | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-oidc.adoc)                           | 3.33.1     |
| quarkus-rest-client-oidc-filter        | [Link](https://quarkus.io/guides/security-openid-connect-client-reference#rest-client-oidc-filter) | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest-client-oidc-filter.adoc)        | 3.33.1     |
| tkit-quarkus-security                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-security.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-security.adoc)                   | 5.1.0      |
| onecx-core                             | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-core.html)           | 3.0.0                                                                                                                                            |            |
| quarkus-arc                            | [Link](https://quarkus.io/guides/cdi-reference)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-arc.adoc)                            | 3.33.1     |
| quarkus-container-image-docker         | [Link](https://quarkus.io/guides/container-image)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-container-image-docker.adoc)         | 3.33.1     |
| quarkus-kubernetes-client              | 3.33.1                                                                                             |                                                                                                                                                  |            |

## [](#%5Fhelm)Helm

[Link to Helm registry](https://github.com/onecx/onecx-data-orchestrator-bff/pkgs/container/charts%2Fonecx-data-orchestrator-bff)

Default values in src/main/helm/values.yaml

```yaml
app:
  serviceAccount:
    enabled: true
  name: bff
  image:
    repository: "onecx/onecx-data-orchestrator-bff"
  envCustom:
    - name: QUARKUS_KUBERNETES_CLIENT_NAMESPACE
      valueFrom:
        fieldRef:
          fieldPath: metadata.namespace
  operator:
    # Permission
    permission:
      enabled: true
      spec:
        permissions:
          crd:
            read: permission on all GET requests and POST search
            write: permission on PUT, POST, PATCH requests, where objects are saved or updated
            touch: permission on PUT request, where a resource is touched
    keycloak:
      client:
        enabled: true
        spec:
          kcConfig:
            defaultClientScopes: [ ocx-pm:read ]
    microservice:
      spec:
        description: OneCX Data Orchestrator Backend for Frontend
        name: OneCX Data Orchestrator BFF
```
