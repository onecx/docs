# undefined

## [](#%5Fonecx%5Ftenant)onecx-tenant

Implementation of the \[tkit-quarkus-rest-context\](<https://github.com/1000kit/tkit-quarkus/blob/main/extensions/rest-context/>) tenant resolver service.

### [](#%5Finstallation)Installation

If you want to use this extension, you need to add the `org.tkit.onecx.quarkus:onecx-tenant` extension first to your build file.

For instance, with Maven, add the following dependency to your POM file:

```xml
<dependency>
    <groupId>org.tkit.onecx.quarkus</groupId>
    <artifactId>onecx-tenant</artifactId>
    <version>3.0.0</version>
</dependency>
```

### [](#%5Fusage)Usage

To activate multi-tenancy also for hibernate, add the following maven dependency to your project \[tkit-quarkus-jpa-tenant\](<https://github.com/1000kit/tkit-quarkus/tree/main/extensions/jpa-tenant>).

```xml
<dependency>
    <groupId>org.tkit.quarkus.lib</groupId>
    <artifactId>tkit-quarkus-jpa-tenant</artifactId>
</dependency>
```

### [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                                                                                                      | Type    | Default                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ---------------------------- |
| [onecx.tenant.cache-enabled](#onecx-tenant%5Fonecx-tenant-cache-enabled) Enable or disable cache for the token Environment variable: ONECX\_TENANT\_CACHE\_ENABLED                                                                                                                          | boolean | true                         |
| [onecx.tenant.service.client.url](#onecx-tenant%5Fonecx-tenant-service-client-url) Tenant client URL configuration. This property is alias for rest-client generated configuration property quarkus.rest-client.onecx\_tenant.url Environment variable: ONECX\_TENANT\_SERVICE\_CLIENT\_URL | string  | http://onecx-tenant-svc:8080 |
