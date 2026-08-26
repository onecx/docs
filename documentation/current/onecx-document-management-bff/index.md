# OneCX Document Backend for Frontend

[Link to Docker registry](https://github.com/onecx/onecx-document-management-bff/pkgs/container/onecx-document-management-bff)

## [](#%5Fdefault%5Fproperties)Default properties

src/main/resources/application.properties 

```properties
quarkus.http.auth.permission.health.paths=/q/*
quarkus.http.auth.permission.health.policy=permit
quarkus.http.auth.permission.default.paths=/*
quarkus.http.auth.permission.default.policy=authenticated
onecx.permissions.application-id=${quarkus.application.name}
%prod.quarkus.rest-client.onecx_document_svc.url = http://onecx-document-management-svc:8080
org.eclipse.microprofile.rest.client.propagateHeaders=apm-principal-token
quarkus.http.limits.max-body-size=20240K
quarkus.openapi-generator.codegen.input-base-dir=target/tmp/openapi
quarkus.openapi-generator.codegen.spec.onecx_document_management_svc_yaml.config-key=onecx_document_svc
quarkus.openapi-generator.codegen.spec.onecx_document_management_svc_yaml.base-package=gen.org.tkit.onecx.document-management.client
quarkus.openapi-generator.codegen.spec.onecx_document_management_svc_yaml.return-response=true
quarkus.openapi-generator.codegen.spec.onecx_document_management_svc_yaml.additional-api-type-annotations=@org.eclipse.microprofile.rest.client.annotation.RegisterClientHeaders;
quarkus.openapi-generator.codegen.spec.onecx_document_management_svc_yaml.enable-security-generation=false
quarkus.openapi-generator.codegen.spec.onecx_document_management_svc_yaml.import-mappings=MultipartFormDataInput=org.jboss.resteasy.reactive.server.multipart.MultipartFormDataInput
quarkus.openapi-generator.codegen.spec.onecx_document_management_svc_yaml.type-mappings.File=java.io.File
quarkus.openapi-generator.codegen.spec.onecx_document_management_svc_yaml.type-mappings.MultipartFormDataInput=org.jboss.resteasy.reactive.server.multipart.MultipartFormDataInput
quarkus.openapi-generator.codegen.spec.onecx_file_storage_svc_yaml.config-key=onecx_file_storage_svc
quarkus.openapi-generator.codegen.spec.onecx_file_storage_svc_yaml.base-package=gen.org.tkit.onecx.filestorage.client
quarkus.openapi-generator.codegen.spec.onecx_file_storage_svc_yaml.return-response=true
quarkus.openapi-generator.codegen.spec.onecx_file_storage_svc_yaml.enable-security-generation=false
onecx.onecx.document.file-storage.product-name=onecx-document-management
onecx.onecx.document.file-storage.application-id=onecx-document-management-bff
onecx.onecx.document.file-storage.file-name-separator=_
%prod.quarkus.rest-client.onecx_document_svc.providers=io.quarkus.oidc.client.reactive.filter.OidcClientRequestReactiveFilter
%prod.quarkus.oidc-client.client-id=${quarkus.application.name}
```

## [](#%5Fextensions)Extensions

Extensions List 

| Extensions                             | Documentation                                                                                      | Configuration                                                                                                                                    | Version    |
| -------------------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- |
| tkit-quarkus-log-rs                    | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-rs.html)       | [Link](https://github.com/1000kit/tkit-quarkus/blob/4.6.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-rs.adoc)                     | 4.6.0      |
| tkit-quarkus-log-cdi                   | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-cdi.html)      | [Link](https://github.com/1000kit/tkit-quarkus/blob/4.6.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-cdi.adoc)                    | 4.6.0      |
| tkit-quarkus-rest                      | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest.html)         | [Link](https://github.com/1000kit/tkit-quarkus/blob/4.6.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest.adoc)                       | 4.6.0      |
| tkit-quarkus-log-json                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-json.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/4.6.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-json.adoc)                   | 4.6.0      |
| tkit-quarkus-rest-context              | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-rest-context.html) | [Link](https://github.com/1000kit/tkit-quarkus/blob/4.6.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-rest-context.adoc)               | 4.6.0      |
| quarkus-rest                           | [Link](https://quarkus.io/guides/rest)                                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest.adoc)                           | 3.27.1     |
| quarkus-rest-jackson                   | [Link](https://quarkus.io/guides/rest-json)                                                        | 3.27.1                                                                                                                                           |            |
| quarkus-rest-client                    | [Link](https://quarkus.io/guides/rest-client)                                                      | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest-client.adoc)                    | 3.27.1     |
| quarkus-smallrye-health                | [Link](https://quarkus.io/guides/smallrye-health)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-health.adoc)                | 3.27.1     |
| quarkus-openapi-generator              | [Link](https://docs.quarkiverse.io/quarkus-openapi-generator/dev/index.html)                       | [Link](https://github.com/quarkiverse/quarkus-openapi-generator/blob/2.13.0-lts/docs/modules/ROOT/pages/includes/quarkus-openapi-generator.adoc) | 2.13.0-lts |
| quarkus-rest-client-jackson            | [Link](https://quarkus.io/guides/rest-client)                                                      | 3.27.1                                                                                                                                           |            |
| quarkus-smallrye-openapi               | [Link](https://quarkus.io/guides/openapi-swaggerui)                                                | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-openapi.adoc)               | 3.27.1     |
| quarkus-hibernate-validator            | [Link](https://quarkus.io/guides/validation)                                                       | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-hibernate-validator.adoc)            | 3.27.1     |
| quarkus-oidc                           | [Link](https://quarkus.io/guides/security-oidc-bearer-token-authentication-tutorial)               | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-oidc.adoc)                           | 3.27.1     |
| quarkus-rest-client-oidc-filter        | [Link](https://quarkus.io/guides/security-openid-connect-client-reference#rest-client-oidc-filter) | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest-client-oidc-filter.adoc)        | 3.27.1     |
| tkit-quarkus-security                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-security.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/4.6.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-security.adoc)                   | 4.6.0      |
| onecx-permissions                      | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-permissions.html)    | [Link](https://github.com/onecx/onecx-quarkus/blob/2.3.0/docs/modules/onecx-quarkus/pages/includes/onecx-permissions.adoc)                       | 2.3.0      |
| onecx-core                             | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-core.html)           | 2.3.0                                                                                                                                            |            |
| quarkus-micrometer-registry-prometheus | [Link](https://quarkus.io/guides/telemetry-micrometer)                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-micrometer-registry-prometheus.adoc) | 3.27.1     |
| quarkus-opentelemetry                  | [Link](https://quarkus.io/guides/opentelemetry)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-opentelemetry.adoc)                  | 3.27.1     |
| quarkus-arc                            | [Link](https://quarkus.io/guides/cdi-reference)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-arc.adoc)                            | 3.27.1     |
| quarkus-container-image-docker         | [Link](https://quarkus.io/guides/container-image)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-container-image-docker.adoc)         | 3.27.1     |

## [](#%5Fhelm)Helm

[Link to Helm registry](https://github.com/onecx/onecx-document-management-bff/pkgs/container/charts%2Fonecx-document-management-bff)

Default values in src/main/helm/values.yaml

```yaml
app:
  image:
    repository: "onecx-apps/onecx-document-management-bff"
    tag: 999-SNAPSHOT
  operator:
    # Permission
    permission:
      enabled: true
      spec:
        permissions:
          document:
            read: permission on all GET requests and POST search
            write: permission on PUT, POST, PATCH requests, where objects are saved or updated
            delete: permission on all DELETE requests
    keycloak:
      client:
        enabled: true
        spec:
          kcConfig:
            defaultClientScopes: [ ocx-doc:all, ocx-doc:read, ocx-doc:write, ocx-pm:read, ocx-fs:write, ocx-fs:read, ocx-fs:delete ]
  product: false
```
