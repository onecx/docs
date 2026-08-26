# undefined

[Link to Docker registry](https://github.com/onecx/onecx-help-bff/pkgs/container/onecx-help-bff)

## [](#%5Fdefault%5Fproperties)Default properties

src/main/resources/application.properties 

```properties
quarkus.http.auth.permission.health.paths=/q/*
quarkus.http.auth.permission.health.policy=permit
quarkus.http.auth.permission.default.paths=/*
quarkus.http.auth.permission.default.policy=authenticated
onecx.permissions.application-id=${quarkus.application.name}
%prod.quarkus.rest-client.onecx_help_svc.url=http://onecx-help-svc:8080
%prod.quarkus.rest-client.onecx_product_store.url=http://onecx-product-store-svc:8080
org.eclipse.microprofile.rest.client.propagateHeaders=apm-principal-token
%prod.quarkus.rest-client.onecx_help_svc.providers=io.quarkus.oidc.client.reactive.filter.OidcClientRequestReactiveFilter
%prod.quarkus.rest-client.onecx_product_store.providers=io.quarkus.oidc.client.reactive.filter.OidcClientRequestReactiveFilter
%prod.quarkus.oidc-client.client-id=${quarkus.application.name}
quarkus.openapi-generator.codegen.spec.onecx_help_svc_yaml.config-key=onecx_help_svc
quarkus.openapi-generator.codegen.spec.onecx_help_svc_yaml.base-package=gen.org.tkit.onecx.help.client
quarkus.openapi-generator.codegen.spec.onecx_help_svc_yaml.return-response=true
quarkus.openapi-generator.codegen.input-base-dir=target/tmp/openapi
quarkus.openapi-generator.codegen.spec.onecx_help_svc_yaml.additional-api-type-annotations=@org.eclipse.microprofile.rest.client.annotation.RegisterClientHeaders;
quarkus.openapi-generator.codegen.spec.onecx_help_svc_yaml.additional-model-type-annotations=@io.quarkus.runtime.annotations.RegisterForReflection;
quarkus.openapi-generator.onecx_help_svc_yaml.auth.oauth2.token-propagation=false
quarkus.openapi-generator.codegen.spec.onecx_help_svc_yaml.enable-security-generation=false
quarkus.openapi-generator.codegen.spec.onecx_help_svc_exim_v1_yaml.config-key=onecx_help_svc
quarkus.openapi-generator.codegen.spec.onecx_help_svc_exim_v1_yaml.base-package=gen.org.tkit.onecx.help.exim.client
quarkus.openapi-generator.codegen.spec.onecx_help_svc_exim_v1_yaml.return-response=true
quarkus.openapi-generator.codegen.spec.onecx_help_svc_exim_v1_yaml.additional-api-type-annotations=@org.eclipse.microprofile.rest.client.annotation.RegisterClientHeaders;
quarkus.openapi-generator.codegen.spec.onecx_help_svc_exim_v1_yaml.additional-model-type-annotations=@io.quarkus.runtime.annotations.RegisterForReflection;
quarkus.openapi-generator.codegen.spec.onecx_help_svc_exim_v1_yaml.enable-security-generation=false
quarkus.openapi-generator.codegen.spec.onecx_product_store_v1_yaml.config-key=onecx_product_store
quarkus.openapi-generator.codegen.spec.onecx_product_store_v1_yaml.base-package=gen.org.tkit.onecx.product.store
quarkus.openapi-generator.codegen.spec.onecx_product_store_v1_yaml.return-response=true
quarkus.openapi-generator.codegen.spec.onecx_product_store_v1_yaml.additional-api-type-annotations=@org.eclipse.microprofile.rest.client.annotation.RegisterClientHeaders;
quarkus.openapi-generator.codegen.spec.onecx_product_store_v1_yaml.additional-model-type-annotations=@io.quarkus.runtime.annotations.RegisterForReflection;
quarkus.openapi-generator.codegen.spec.onecx_product_store_v1_yaml.enable-security-generation=false
```

## [](#%5Fextensions)Extensions

Extensions List 

| Extensions                             | Documentation                                                                                      | Configuration                                                                                                                                    | Version    |
| -------------------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- |
| quarkus-rest                           | [Link](https://quarkus.io/guides/rest)                                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest.adoc)                           | 3.33.1     |
| quarkus-smallrye-openapi               | [Link](https://quarkus.io/guides/openapi-swaggerui)                                                | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-openapi.adoc)               | 3.33.1     |
| quarkus-rest-jackson                   | [Link](https://quarkus.io/guides/rest-json)                                                        | 3.33.1                                                                                                                                           |            |
| quarkus-openapi-generator              | [Link](https://docs.quarkiverse.io/quarkus-openapi-generator/dev/index.html)                       | [Link](https://github.com/quarkiverse/quarkus-openapi-generator/blob/2.16.0-lts/docs/modules/ROOT/pages/includes/quarkus-openapi-generator.adoc) | 2.16.0-lts |
| quarkus-rest-client-jackson            | [Link](https://quarkus.io/guides/rest-client)                                                      | 3.33.1                                                                                                                                           |            |
| tkit-quarkus-log-cdi                   | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-cdi.html)      | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-cdi.adoc)                    | 5.1.0      |
| tkit-quarkus-log-rs                    | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-rs.html)       | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-rs.adoc)                     | 5.1.0      |
| tkit-quarkus-log-json                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-json.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-json.adoc)                   | 5.1.0      |
| tkit-quarkus-rest                      | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest.html)         | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest.adoc)                       | 5.1.0      |
| tkit-quarkus-rest-context              | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest-context.html) | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest-context.adoc)               | 5.1.0      |
| quarkus-hibernate-validator            | [Link](https://quarkus.io/guides/validation)                                                       | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-hibernate-validator.adoc)            | 3.33.1     |
| quarkus-smallrye-health                | [Link](https://quarkus.io/guides/smallrye-health)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-health.adoc)                | 3.33.1     |
| quarkus-opentelemetry                  | [Link](https://quarkus.io/guides/opentelemetry)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-opentelemetry.adoc)                  | 3.33.1     |
| quarkus-micrometer-registry-prometheus | [Link](https://quarkus.io/guides/telemetry-micrometer)                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-micrometer-registry-prometheus.adoc) | 3.33.1     |
| quarkus-oidc                           | [Link](https://quarkus.io/guides/security-oidc-bearer-token-authentication-tutorial)               | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-oidc.adoc)                           | 3.33.1     |
| quarkus-rest-client-oidc-filter        | [Link](https://quarkus.io/guides/security-openid-connect-client-reference#rest-client-oidc-filter) | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest-client-oidc-filter.adoc)        | 3.33.1     |
| onecx-permissions                      | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-permissions.html)    | [Link](https://github.com/onecx/onecx-quarkus/blob/3.0.0/docs/modules/onecx-quarkus/pages/includes/onecx-permissions.adoc)                       | 3.0.0      |
| tkit-quarkus-security                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-security.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-security.adoc)                   | 5.1.0      |
| onecx-core                             | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-core.html)           | 3.0.0                                                                                                                                            |            |
| quarkus-arc                            | [Link](https://quarkus.io/guides/cdi-reference)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-arc.adoc)                            | 3.33.1     |
| quarkus-container-image-docker         | [Link](https://quarkus.io/guides/container-image)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-container-image-docker.adoc)         | 3.33.1     |
| quarkus-oidc-client                    | 3.33.1                                                                                             |                                                                                                                                                  |            |

## [](#%5Fhelm)Helm

[Link to Helm registry](https://github.com/onecx/onecx-help-bff/pkgs/container/charts%2Fonecx-help-bff)

Default values in src/main/helm/values.yaml

```yaml
app:
  name: bff
  image:
    repository: "onecx/onecx-help-bff"
  operator:
    # Permission
    permission:
      enabled: true
      spec:
        permissions:
          help:
            read: permission on all GET requests and POST search
            write: permission on PUT, POST, PATCH requests, where objects are saved or updated
            delete: permission on all DELETE requests
          product:
            read: permission on all GET requests and POST search
    keycloak:
      client:
        enabled: true
        spec:
          kcConfig:
            defaultClientScopes: [ ocx-hp:all, ocx-ps:read, ocx-pm:read ]
    microservice:
      spec:
        description: OneCX Help Backend For Frontend
        name: OneCX Help BFF
```
