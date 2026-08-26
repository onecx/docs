# OneCX IAM Keycloak Client Operator

## [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                                                                                             | Type               | Default                            |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ | ---------------------------------- |
| [onecx.iam.kc.client.realm](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-realm) Define realm where to insert/update/delete the clients Environment variable: ONECX\_IAM\_KC\_CLIENT\_REALM                                                                                  | string             | onecx                              |
| [onecx.iam.kc.client.config."config".add-def-scopes](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-add-def-scopes) Add default scopes from realm to the client. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_ADD\_DEF\_SCOPES             | boolean            | true                               |
| [onecx.iam.kc.client.config."config".enabled](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-enabled) Enable the client Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_ENABLED                                                               | boolean            | true                               |
| [onecx.iam.kc.client.config."config".auth-type](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-auth-type) Authentication type. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_AUTH\_TYPE                                                     | string             | client-secret                      |
| [onecx.iam.kc.client.config."config".redirect-uris](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-redirect-uris) List of redirect uris. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_REDIRECT\_URIS                                       | list of string     |                                    |
| [onecx.iam.kc.client.config."config".web-origins](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-web-origins) List of web origins Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_WEB\_ORIGINS                                                | list of string     |                                    |
| [onecx.iam.kc.client.config."config".bearer-only](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-bearer-only) Bearer token only. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_BEARER\_ONLY                                                 | boolean            | false                              |
| [onecx.iam.kc.client.config."config".standard-flow](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-standard-flow) Standard flow enabled. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_STANDARD\_FLOW                                       | boolean            | false                              |
| [onecx.iam.kc.client.config."config".implicit-flow](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-implicit-flow) Implicit flow enabled. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_IMPLICIT\_FLOW                                       | boolean            | false                              |
| [onecx.iam.kc.client.config."config".direct-access](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-direct-access) Enable direct access grants. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_DIRECT\_ACCESS                                 | boolean            | false                              |
| [onecx.iam.kc.client.config."config".service-account](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-service-account) Enable service account. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_SERVICE\_ACCOUNT                                | boolean            | true                               |
| [onecx.iam.kc.client.config."config".public](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-public) Public client flag. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_PUBLIC                                                                | boolean            | false                              |
| [onecx.iam.kc.client.config."config".protocol](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-protocol) Protocol used with the client. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_PROTOCOL                                               | string             | openid-connect                     |
| [onecx.iam.kc.client.config."config".attributes."attributes"](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-attributes-attributes) Attributes map for the client. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_ATTRIBUTES\_\_ATTRIBUTES\_ | Map<String,String> |                                    |
| [onecx.iam.kc.client.config."config".default-scopes](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-default-scopes) Default client scopes. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_DEFAULT\_SCOPES                                    | list of string     |                                    |
| [onecx.iam.kc.client.config."config".optional-scopes](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-config-config-optional-scopes) Optional client scopes. Environment variable: ONECX\_IAM\_KC\_CLIENT\_CONFIG\_\_CONFIG\_\_OPTIONAL\_SCOPES                                | list of string     |                                    |
| [onecx.iam.kc.client.leader-election.lease-name](#onecx-iam-kc-client-operator%5Fonecx-iam-kc-client-leader-election-lease-name) Lease name Environment variable: ONECX\_IAM\_KC\_CLIENT\_LEADER\_ELECTION\_LEASE\_NAME                                                            | string             | onecx-iam-kc-client-operator-lease |

[Link to Docker registry](https://github.com/onecx/onecx-iam-kc-client-operator/pkgs/container/onecx-iam-kc-client-operator)

## [](#%5Fdefault%5Fproperties)Default properties

src/main/resources/application.properties 

```properties
quarkus.kubernetes-client.devservices.override-kubeconfig=true
quarkus.keycloak.admin-client.server-url=http://keycloak:8080
quarkus.keycloak.admin-client.realm=master
quarkus.keycloak.admin-client.username=admin
quarkus.operator-sdk.controllers.kc.retry.max-attempts=10
quarkus.operator-sdk.controllers.kc.retry.interval.initial=5000
quarkus.operator-sdk.controllers.kc.retry.interval.multiplier=3
quarkus.operator-sdk.controllers.kc.retry.interval.max=300000
quarkus.operator-sdk.crd.validate=false
quarkus.operator-sdk.helm.enabled=true
onecx.iam.kc.client.realm=onecx
onecx.iam.kc.client.config.ui.enabled=true
onecx.iam.kc.client.config.ui.auth-type=client-secret
onecx.iam.kc.client.config.ui.redirect-uris=*
onecx.iam.kc.client.config.ui.web-origins=*
onecx.iam.kc.client.config.ui.bearer-only=false
onecx.iam.kc.client.config.ui.standard-flow=true
onecx.iam.kc.client.config.ui.implicit-flow=false
onecx.iam.kc.client.config.ui.direct-access=true
onecx.iam.kc.client.config.ui.service-account=false
onecx.iam.kc.client.config.ui.protocol=openid-connect
onecx.iam.kc.client.config.ui.default-scopes=web-origins,roles,profile,email
onecx.iam.kc.client.config.ui.public=true
onecx.iam.kc.client.config.ui.add-def-scopes=true
onecx.iam.kc.client.config.machine.enabled=true
onecx.iam.kc.client.config.machine.auth-type=client-secret
onecx.iam.kc.client.config.machine.bearer-only=false
onecx.iam.kc.client.config.machine.standard-flow=false
onecx.iam.kc.client.config.machine.implicit-flow=false
onecx.iam.kc.client.config.machine.direct-access=false
onecx.iam.kc.client.config.machine.service-account=true
onecx.iam.kc.client.config.machine.protocol=openid-connect
onecx.iam.kc.client.config.machine.default-scopes=web-origins,roles,profile,email
onecx.iam.kc.client.config.machine.public=false
onecx.iam.kc.client.config.machine.add-def-scopes=true
```

## [](#%5Fextensions)Extensions

Extensions List 

| Extensions                             | Documentation                                                                                  | Configuration                                                                                                                                    | Version |
| -------------------------------------- | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------- |
| tkit-quarkus-log-cdi                   | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-cdi.html)  | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-cdi.adoc)                    | 5.1.0   |
| tkit-quarkus-log-rs                    | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-rs.html)   | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-rs.adoc)                     | 5.1.0   |
| tkit-quarkus-log-json                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-log-json.html) | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-log-json.adoc)                   | 5.1.0   |
| quarkus-arc                            | [Link](https://quarkus.io/guides/cdi-reference)                                                | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-arc.adoc)                            | 3.33.1  |
| quarkus-micrometer-registry-prometheus | [Link](https://quarkus.io/guides/telemetry-micrometer)                                         | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-micrometer-registry-prometheus.adoc) | 3.33.1  |
| quarkus-opentelemetry                  | [Link](https://quarkus.io/guides/opentelemetry)                                                | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-opentelemetry.adoc)                  | 3.33.1  |
| quarkus-rest-client                    | [Link](https://quarkus.io/guides/rest-client)                                                  | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-rest-client.adoc)                    | 3.33.1  |
| quarkus-rest-client-jackson            | [Link](https://quarkus.io/guides/rest-client)                                                  | 3.33.1                                                                                                                                           |         |
| tkit-quarkus-security                  | [Link](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-security.html) | [Link](https://github.com/1000kit/tkit-quarkus/blob/5.1.0/docs/modules/tkit-quarkus/pages/includes/tkit-quarkus-security.adoc)                   | 5.1.0   |
| onecx-core                             | [Link](https://onecx.github.io/docs/onecx-quarkus/current/onecx-quarkus/onecx-core.html)       | 3.0.0                                                                                                                                            |         |
| quarkus-smallrye-health                | [Link](https://quarkus.io/guides/smallrye-health)                                              | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-smallrye-health.adoc)                | 3.33.1  |
| quarkus-container-image-docker         | [Link](https://quarkus.io/guides/container-image)                                              | [Link](https://github.com/quarkusio/quarkusio.github.io/blob/develop/%5Fgenerated-doc/latest/config/quarkus-container-image-docker.adoc)         | 3.33.1  |
| quarkus-operator-sdk-bundle-generator  | 7.7.3                                                                                          |                                                                                                                                                  |         |
| quarkus-operator-sdk                   | 7.7.3                                                                                          |                                                                                                                                                  |         |
| onecx-operator                         | 3.0.0                                                                                          |                                                                                                                                                  |         |
| quarkus-keycloak-admin-rest-client     | 3.33.1                                                                                         |                                                                                                                                                  |         |

## [](#%5Fhelm)Helm

[Link to Helm registry](https://github.com/onecx/onecx-iam-kc-client-operator/pkgs/container/charts%2Fonecx-iam-kc-client-operator)

Default values in src/main/helm/values.yaml

```yaml
app:
  name: kc-client-operator
  image:
    repository: "onecx/onecx-iam-kc-client-operator"
  envCustom:
    - name: KUBERNETES_NAMESPACE
      valueFrom:
        fieldRef:
          fieldPath: metadata.namespace
  serviceAccount:
    enabled: true
  operator:
    microservice:
      spec:
        description: OneCX IAM Keycloak Client Operator
        name: OneCX IAM KC Client Operator
```
