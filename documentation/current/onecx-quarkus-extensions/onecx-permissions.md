# undefined

## [](#%5Fonecx%5Fpermissions)onecx-permissions

### [](#%5Finstallation)Installation

If you want to use this extension, you need to add the `org.tkit.onecx.quarkus:onecx-permission` extension first to your build file.

For instance, with Maven, add the following dependency to your POM file:

```xml
<dependency>
    <groupId>org.tkit.onecx.quarkus</groupId>
    <artifactId>onecx-permission</artifactId>
    <version>3.0.0</version>
</dependency>
```

### [](#%5Fusage)Usage

1. First you need to add the maven dependency shown at the top
2. Then you can use @PermissionsAllowed annotation

```java
    @GET
    @Path("write")
    @PermissionsAllowed(value = "onecx:resource#action")
    public Response adminWrite() {
        return Response.ok("OK").build();
    }
```

### [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                                                                                                                              | Type                                 | Default                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ | --------------------------------------------------------- |
| [onecx.permissions.service.client.url](#onecx-permissions%5Fonecx-permissions-service-client-url) Tenant client URL configuration. This property is alias for rest-client generated configuration property quarkus.rest-client.onecx\_permission.url Environment variable: ONECX\_PERMISSIONS\_SERVICE\_CLIENT\_URL | string                               | http://onecx-permission-svc:8080                          |
| [onecx.permissions.enabled](#onecx-permissions%5Fonecx-permissions-enabled) Enable interface mapping Environment variable: ONECX\_PERMISSIONS\_ENABLED                                                                                                                                                              | boolean                              | true                                                      |
| [onecx.permissions.cache-enabled](#onecx-permissions%5Fonecx-permissions-cache-enabled) Enable interface mapping Environment variable: ONECX\_PERMISSIONS\_CACHE\_ENABLED                                                                                                                                           | boolean                              | true                                                      |
| [onecx.permissions.allow-all](#onecx-permissions%5Fonecx-permissions-allow-all) Allow all permissions Environment variable: ONECX\_PERMISSIONS\_ALLOW\_ALL                                                                                                                                                          | boolean                              | false                                                     |
| [onecx.permissions.product-name](#onecx-permissions%5Fonecx-permissions-product-name) Product name. Environment variable: ONECX\_PERMISSIONS\_PRODUCT\_NAME                                                                                                                                                         | string                               | required                                                  |
| [onecx.permissions.application-id](#onecx-permissions%5Fonecx-permissions-application-id) Permissions application ID. Environment variable: ONECX\_PERMISSIONS\_APPLICATION\_ID                                                                                                                                     | string                               | ${quarkus.application.name}                               |
| [onecx.permissions.name](#onecx-permissions%5Fonecx-permissions-name) Permissions prefix name. Environment variable: ONECX\_PERMISSIONS\_NAME                                                                                                                                                                       | string                               | onecx                                                     |
| [onecx.permissions.request-token-from-header-param](#onecx-permissions%5Fonecx-permissions-request-token-from-header-param) Permissions access token header parameter. Environment variable: ONECX\_PERMISSIONS\_REQUEST\_TOKEN\_FROM\_HEADER\_PARAM                                                                | string                               | Authorization                                             |
| [onecx.permissions.token-header-param](#onecx-permissions%5Fonecx-permissions-token-header-param) Permissions principal token header parameter. Environment variable: ONECX\_PERMISSIONS\_TOKEN\_HEADER\_PARAM                                                                                                      | string                               | ${tkit.rs.context.token.header-param:apm-principal-token} |
| [onecx.permissions.key-separator](#onecx-permissions%5Fonecx-permissions-key-separator) Permissions resource action separator. Environment variable: ONECX\_PERMISSIONS\_KEY\_SEPARATOR                                                                                                                             | string                               | #                                                         |
| [onecx.permissions.mock.enabled](#onecx-permissions%5Fonecx-permissions-mock-enabled) Enable or disable mock service Environment variable: ONECX\_PERMISSIONS\_MOCK\_ENABLED                                                                                                                                        | boolean                              | false                                                     |
| [onecx.permissions.mock.roles."roles"](#onecx-permissions%5Fonecx-permissions-mock-roles-roles) Mock data for role Map format : \[role\].\[permission\]=\[actions\] Environment variable: ONECX\_PERMISSIONS\_MOCK\_ROLES\_\_ROLES\_                                                                                | Map<String,Map<String,List<String>>> |                                                           |
