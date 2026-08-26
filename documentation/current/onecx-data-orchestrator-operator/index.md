# OneCX Data Orchestrator Operator

## [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                                                                                                               | Type               | Default                                |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ | -------------------------------------- |
| [onecx.data-orchestrator.digest](#onecx-data-orchestrator-operator%5Fonecx-data-orchestrator-digest) Digest algorithms. Environment variable: ONECX\_DATA\_ORCHESTRATOR\_DIGEST                                                                                                                      | string             | MD5                                    |
| [onecx.data-orchestrator.token.user-name](#onecx-data-orchestrator-operator%5Fonecx-data-orchestrator-token-user-name) Username for rest call. Environment variable: ONECX\_DATA\_ORCHESTRATOR\_TOKEN\_USER\_NAME                                                                                    | string             | data-orchestrator-operator             |
| [onecx.data-orchestrator.token.header-param](#onecx-data-orchestrator-operator%5Fonecx-data-orchestrator-token-header-param) Token header parameter. Environment variable: ONECX\_DATA\_ORCHESTRATOR\_TOKEN\_HEADER\_PARAM                                                                           | string             | apm-principal-token                    |
| [onecx.data-orchestrator.token.claim-organization-param](#onecx-data-orchestrator-operator%5Fonecx-data-orchestrator-token-claim-organization-param) Token claim organization parameter. Environment variable: ONECX\_DATA\_ORCHESTRATOR\_TOKEN\_CLAIM\_ORGANIZATION\_PARAM                          | string             | orgId                                  |
| [onecx.data-orchestrator.token.claim-organization-param-array](#onecx-data-orchestrator-operator%5Fonecx-data-orchestrator-token-claim-organization-param-array) Token claim organization parameter array. Environment variable: ONECX\_DATA\_ORCHESTRATOR\_TOKEN\_CLAIM\_ORGANIZATION\_PARAM\_ARRAY | boolean            | false                                  |
| [onecx.data-orchestrator.client.shared](#onecx-data-orchestrator-operator%5Fonecx-data-orchestrator-client-shared) Set to true to share the HTTP client between REST clients. Environment variable: ONECX\_DATA\_ORCHESTRATOR\_CLIENT\_SHARED                                                        | boolean            | true                                   |
| [onecx.data-orchestrator.client.connection-pool-size](#onecx-data-orchestrator-operator%5Fonecx-data-orchestrator-client-connection-pool-size) The size of the rest client connection pool. Environment variable: ONECX\_DATA\_ORCHESTRATOR\_CLIENT\_CONNECTION\_POOL\_SIZE                          | int                | 30                                     |
| [onecx.data-orchestrator.client.key."keys"](#onecx-data-orchestrator-operator%5Fonecx-data-orchestrator-client-key-keys) Clients key configuration Environment variable: ONECX\_DATA\_ORCHESTRATOR\_CLIENT\_KEY\_\_KEYS\_                                                                            | Map<String,String> |                                        |
| [onecx.data-orchestrator.leader-election.lease-name](#onecx-data-orchestrator-operator%5Fonecx-data-orchestrator-leader-election-lease-name) Lease name Environment variable: ONECX\_DATA\_ORCHESTRATOR\_LEADER\_ELECTION\_LEASE\_NAME                                                               | string             | onecx-data-orchestrator-operator-lease |

[Link to Docker registry](https://github.com/onecx/onecx-data-orchestrator-operator/pkgs/container/onecx-data-orchestrator-operator)

## [](#%5Fdefault%5Fproperties)Default properties

src/main/resources/application.properties 

```properties
onecx.data-orchestrator.client.key.workspace=http://onecx-workspace-svc:8080/exim/v1/workspace/operator
onecx.data-orchestrator.client.key.theme=http://onecx-theme-svc:8080/exim/v1/themes/operator
onecx.data-orchestrator.client.key.tenant=http://onecx-tenant-svc:8080/exim/v1/tenants/operator
onecx.data-orchestrator.client.key.permission=http://onecx-permission-svc:8080/exim/v1/assignments/operator
onecx.data-orchestrator.client.key.help=http://onecx-help-svc:8080/exim/v1/help/operator
quarkus.operator-sdk.controllers.data.retry.max-attempts=10
quarkus.operator-sdk.controllers.data.retry.interval.initial=5000
quarkus.operator-sdk.controllers.data.retry.interval.multiplier=3
quarkus.operator-sdk.controllers.data.retry.interval.max=300000
quarkus.operator-sdk.controllers.data.namespaces=JOSDK_WATCH_CURRENT
quarkus.operator-sdk.crd.validate=false
quarkus.operator-sdk.helm.enabled=true
quarkus.kubernetes-client.devservices.override-kubeconfig=true
%prod.quarkus.oidc-client.client-id=${quarkus.application.name}
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
| quarkus-oidc                           | [Link](https://quarkus.io/guides/security-oidc-bearer-token-authentication-tutorial)               | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-oidc.adoc)                           | 3.33.1     |
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

[Link to Helm registry](https://github.com/onecx/onecx-data-orchestrator-operator/pkgs/container/charts%2Fonecx-data-orchestrator-operator)

Default values in src/main/helm/values.yaml

```yaml
app:
  name: operator
  image:
    repository: "onecx/onecx-data-orchestrator-operator"
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
            defaultClientScopes: [ ocx-ws:write, ocx-pm:write, ocx-pm-assignment:write, ocx-tn:write, ocx-th:write, ocx-hp:write ]
    microservice:
      spec:
        description: OneCX Data Orchestrator Operator
        name: OneCX Data Orchestrator Operator
```
