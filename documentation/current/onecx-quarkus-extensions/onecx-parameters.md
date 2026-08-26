# undefined

## [](#%5Fonecx%5Fparameters)onecx-parameters

## [](#%5Finstallation)Installation

If you want to use this extension, you need to add the `org.tkit.onecx.quarkus:onecx-parameters` extension first to your build file.

For instance, with Maven, add the following dependency to your POM file:

```xml
<dependency>
    <groupId>org.tkit.onecx.quarkus</groupId>
    <artifactId>onecx-parameters</artifactId>
    <version>3.0.0</version>
</dependency>
```

## [](#%5Fusage)Usage

### [](#%5Fparameter%5Fclient)Parameter client

Assuming you have `Parameters` running on localhost:8088 you should add the following properties to your application.properties and fill in the values for url.

```properties
onecx.parameters.service.client.url=http://localhost:8088/api
```

Once you have configured the properties, you can start using a Parameters-client.

```java
@ApplicationScoped
public class TestService {

    @Inject
    ParametersService parameters;

    public boolean isTest() {
        return parameters.getValue("key", String.class, "DEFAULT_VALUE");
    }
}
```

### [](#%5Fparameter)@Parameter

By using the `@Parameter` annotation there is a shortcut to inject value of the parameter.

```java
@ApplicationScoped
public class TestService {

    @Parameter(name = "param-name-1")
    Instance<Variant> param1;

    @Parameter(name = "param-name-2")
    Instance<String> param2;

    @Parameter(name = "param-name-3")
    Instance<MyCustomJsonModel> param3;

}
```

| |  @Parameter should only be used with the Instance<?> type. |
| ------------------------------------------------------------ |

### [](#%5Fhistory)History

By default, the client will send history of used parameters to the backend. History contains count of usage of the parameter in the interval configure by the `onecx.parameters.history.update-schedule` property.

### [](#%5Fcache)Cache

To avoid to many calls the client will use local cache for parameters. To disable the local cache you can use this property `onecx.parameters.cache.enabled`. The local cache is updated via the scheduler and schedule time is configurable with `onecx.parameters.cache.update-schedule` property.

You can update cache at start of the application `onecx.parameters.cache.update-at-start` and control if the application should not start if there is error to update cache at the start `onecx.parameters.cache.failed-at-start`.

### [](#%5Fmulti%5Ftenancy)Multi-tenancy

To disable or enable multi-tenancy you can use this property `onecx.parameters.tenant.enabled`. To resolve the tenant the [ApplicationContext](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/tkit-quarkus-context.html) will be used.

For background job like cache update you need to implement `@org.tkit.onecx.quarkus.parameter.tenant.TenantResolver` and create ApplicationContext for each cache update.

### [](#%5Fmetrics)Metrics

Micrometer metrics are support by the client library. By default, there are

* parameter usage count `onecx_parameters_item_total`
* update parameters background job counter with response codes `onecx_parameters_update_total`
* send history background job counter with response codes `onecx_parameters_history_total`

### [](#%5Fvalue%5Fconfiguration%5Fpriority)Value configuration priority

You retrieve either the value from the…​

1. Backend parameter service.
2. Project application.properties See: [Quarkus configuration reference guide](https://quarkus.io/guides/config-reference)
3. Source code default value.

in this respective order.

### [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                                                                                                                             | Type               | Default                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------ | --------------------------------------------------------- |
| [onecx.parameters.build.metrics.enabled](#onecx-parameters%5Fonecx-parameters-build-metrics-enabled) Whether a metrics is enabled in case the micrometer or micro-profile metrics extension is present. Environment variable: ONECX\_PARAMETERS\_BUILD\_METRICS\_ENABLED                                           | boolean            | true                                                      |
| [onecx.parameters.service.client.url](#onecx-parameters%5Fonecx-parameters-service-client-url) Parameters client URL configuration. This property is alias for rest-client generated configuration property quarkus.rest-client.onecx\_parameter.url Environment variable: ONECX\_PARAMETERS\_SERVICE\_CLIENT\_URL | string             | http://onecx-parameter-svc:8080                           |
| [onecx.parameters.enabled](#onecx-parameters%5Fonecx-parameters-enabled) If set to true, the application will attempt to look up the configuration from Parameter service Environment variable: ONECX\_PARAMETERS\_ENABLED                                                                                         | boolean            | true                                                      |
| [onecx.parameters.token-header-param](#onecx-parameters%5Fonecx-parameters-token-header-param) Parameters principal token header parameter. Environment variable: ONECX\_PARAMETERS\_TOKEN\_HEADER\_PARAM                                                                                                          | string             | ${tkit.rs.context.token.header-param:apm-principal-token} |
| [onecx.parameters.throw-update-exception](#onecx-parameters%5Fonecx-parameters-throw-update-exception) Throw update exception when parameters are loaded from backend. Environment variable: ONECX\_PARAMETERS\_THROW\_UPDATE\_EXCEPTION                                                                           | boolean            | false                                                     |
| [onecx.parameters.cache.enabled](#onecx-parameters%5Fonecx-parameters-cache-enabled) Enable or disable client cache. Environment variable: ONECX\_PARAMETERS\_CACHE\_ENABLED                                                                                                                                       | boolean            | true                                                      |
| [onecx.parameters.cache.update-schedule](#onecx-parameters%5Fonecx-parameters-cache-update-schedule) Update parameter scheduler configuration in milliseconds. Environment variable: ONECX\_PARAMETERS\_CACHE\_UPDATE\_SCHEDULE                                                                                    | long               | 900000                                                    |
| [onecx.parameters.cache.update-at-start](#onecx-parameters%5Fonecx-parameters-cache-update-at-start) Pull parameters during start phase Environment variable: ONECX\_PARAMETERS\_CACHE\_UPDATE\_AT\_START                                                                                                          | boolean            | false                                                     |
| [onecx.parameters.cache.failed-at-start](#onecx-parameters%5Fonecx-parameters-cache-failed-at-start) Does not start the microservices if an error occurs while retrieving the parameters during the startup phase. Environment variable: ONECX\_PARAMETERS\_CACHE\_FAILED\_AT\_START                               | boolean            | false                                                     |
| [onecx.parameters.product-name](#onecx-parameters%5Fonecx-parameters-product-name) Product name. Environment variable: ONECX\_PARAMETERS\_PRODUCT\_NAME                                                                                                                                                            | string             | required                                                  |
| [onecx.parameters.application-id](#onecx-parameters%5Fonecx-parameters-application-id) Parameters application ID. Environment variable: ONECX\_PARAMETERS\_APPLICATION\_ID                                                                                                                                         | string             | ${quarkus.application.name}                               |
| [onecx.parameters.instance-id](#onecx-parameters%5Fonecx-parameters-instance-id) Instance ID Environment variable: ONECX\_PARAMETERS\_INSTANCE\_ID                                                                                                                                                                 | string             |                                                           |
| [onecx.parameters.history.enabled](#onecx-parameters%5Fonecx-parameters-history-enabled) If set to true, the application will send history information to the parameter management. Environment variable: ONECX\_PARAMETERS\_HISTORY\_ENABLED                                                                      | boolean            | true                                                      |
| [onecx.parameters.history.update-schedule](#onecx-parameters%5Fonecx-parameters-history-update-schedule) Update history scheduler configuration in milliseconds. Environment variable: ONECX\_PARAMETERS\_HISTORY\_UPDATE\_SCHEDULE                                                                                | long               | 900000                                                    |
| [onecx.parameters.items."parameters"](#onecx-parameters%5Fonecx-parameters-items-parameters) Parameters configuration Environment variable: ONECX\_PARAMETERS\_ITEMS\_\_PARAMETERS\_                                                                                                                               | Map<String,String> |                                                           |
| [onecx.parameters.tenant.enabled](#onecx-parameters%5Fonecx-parameters-tenant-enabled) Enable or disable multi-tenancy. Environment variable: ONECX\_PARAMETERS\_TENANT\_ENABLED                                                                                                                                   | boolean            | true                                                      |
