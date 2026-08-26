# OneCX Product Store Operator

## [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                                                             | Type   | Default                            |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ---------------------------------- |
| [onecx.product-store.operator.leader-election.lease-name](#onecx-product-store-operator%5Fonecx-product-store-operator-leader-election-lease-name) Lease name Environment variable: ONECX\_PRODUCT\_STORE\_OPERATOR\_LEADER\_ELECTION\_LEASE\_NAME | string | onecx-product-store-operator-lease |

[Link to Docker registry](https://github.com/onecx/onecx-product-store-operator/pkgs/container/onecx-product-store-operator)

## [](#%5Fdefault%5Fproperties)Default properties

src/main/resources/application.properties 

```properties
quarkus.operator-sdk.controllers.product.retry.max-attempts=10
quarkus.operator-sdk.controllers.product.retry.interval.initial=5000
quarkus.operator-sdk.controllers.product.retry.interval.multiplier=3
quarkus.operator-sdk.controllers.product.retry.interval.max=300000
quarkus.kubernetes-client.devservices.override-kubeconfig=true
%prod.quarkus.rest-client.product_store_client.url=http://onecx-product-store-svc:8080
%prod.quarkus.rest-client.product_store_client.providers=io.quarkus.oidc.client.reactive.filter.OidcClientRequestReactiveFilter
%prod.quarkus.oidc-client.client-id=${quarkus.application.name}
quarkus.operator-sdk.crd.validate=false
quarkus.operator-sdk.helm.enabled=true
quarkus.openapi-generator.codegen.input-base-dir=target/tmp/openapi
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_product_v1_yaml.config-key=product_store_client
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_product_v1_yaml.base-package=gen.org.tkit.onecx.product.store.product.v1
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_product_v1_yaml.return-response=true
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_product_v1_yaml.enable-security-generation=false
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_slot_v1_yaml.config-key=product_store_client
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_slot_v1_yaml.base-package=gen.org.tkit.onecx.product.store.slot.v1
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_slot_v1_yaml.return-response=true
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_slot_v1_yaml.enable-security-generation=false
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_ms_v1_yaml.config-key=product_store_client
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_ms_v1_yaml.base-package=gen.org.tkit.onecx.product.store.ms.v1
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_ms_v1_yaml.return-response=true
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_ms_v1_yaml.enable-security-generation=false
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_mfe_v1_yaml.config-key=product_store_client
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_mfe_v1_yaml.base-package=gen.org.tkit.onecx.product.store.mfe.v1
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_mfe_v1_yaml.return-response=true
quarkus.openapi-generator.codegen.spec.onecx_product_store_operator_mfe_v1_yaml.enable-security-generation=false
```

## [](#%5Fextensions)Extensions

Extensions List 

| Extensions                             | Documentation                                                                                      | Configuration                                                                                                                                    | Version    |
| -------------------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- |
| tkit-quarkus-log-cdi                   | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-cdi.html)      | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-cdi.adoc)                    | 5.1.0      |
| tkit-quarkus-log-rs                    | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-rs.html)       | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-rs.adoc)                     | 5.1.0      |
| tkit-quarkus-log-json                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-json.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-json.adoc)                   | 5.1.0      |
| quarkus-arc                            | [Link](https://quarkus.io/guides/cdi-reference)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-arc.adoc)                            | 3.33.1     |
| quarkus-micrometer-registry-prometheus | [Link](https://quarkus.io/guides/telemetry-micrometer)                                             | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-micrometer-registry-prometheus.adoc) | 3.33.1     |
| quarkus-opentelemetry                  | [Link](https://quarkus.io/guides/opentelemetry)                                                    | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-opentelemetry.adoc)                  | 3.33.1     |
| quarkus-openapi-generator              | [Link](https://docs.quarkiverse.io/quarkus-openapi-generator/dev/index.html)                       | [Link](https://github.com/quarkiverse/quarkus-openapi-generator/blob/2.16.0-lts/docs/modules/ROOT/pages/includes/quarkus-openapi-generator.adoc) | 2.16.0-lts |
| quarkus-rest-client                    | [Link](https://quarkus.io/guides/rest-client)                                                      | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest-client.adoc)                    | 3.33.1     |
| quarkus-rest-client-jackson            | [Link](https://quarkus.io/guides/rest-client)                                                      | 3.33.1                                                                                                                                           |            |
| quarkus-rest-client-oidc-filter        | [Link](https://quarkus.io/guides/security-openid-connect-client-reference#rest-client-oidc-filter) | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest-client-oidc-filter.adoc)        | 3.33.1     |
| tkit-quarkus-security                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-security.html)     | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-security.adoc)                   | 5.1.0      |
| onecx-core                             | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-core.html)           | 3.0.0                                                                                                                                            |            |
| quarkus-smallrye-health                | [Link](https://quarkus.io/guides/smallrye-health)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-health.adoc)                | 3.33.1     |
| quarkus-container-image-docker         | [Link](https://quarkus.io/guides/container-image)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-container-image-docker.adoc)         | 3.33.1     |
| quarkus-operator-sdk-bundle-generator  | 7.7.3                                                                                              |                                                                                                                                                  |            |
| quarkus-operator-sdk                   | 7.7.3                                                                                              |                                                                                                                                                  |            |
| onecx-operator                         | 3.0.0                                                                                              |                                                                                                                                                  |            |
| quarkus-openapi-generator-oidc         | 2.16.0-lts                                                                                         |                                                                                                                                                  |            |
| quarkus-oidc-client                    | 3.33.1                                                                                             |                                                                                                                                                  |            |

## [](#%5Fhelm)Helm

[Link to Helm registry](https://github.com/onecx/onecx-product-store-operator/pkgs/container/charts%2Fonecx-product-store-operator)

Default values in src/main/helm/values.yaml

```yaml
app:
  name: product-operator
  image:
    repository: "onecx/onecx-product-store-operator"
  envCustom:
    - name: KUBERNETES_NAMESPACE
      valueFrom:
        fieldRef:
          fieldPath: metadata.namespace
  serviceAccount:
    enabled: true
  operator:
    keycloak:
      client:
        enabled: true
        spec:
          kcConfig:
            defaultClientScopes: [ ocx-ps-product:write, ocx-ps-slot:write, ocx-ps-ms:write, ocx-ps-mfe:write ]
    microservice:
      spec:
        description: OneCX Product Store Operator
        name: OneCX Product Store Operator
```
