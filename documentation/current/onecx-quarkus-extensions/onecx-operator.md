# undefined

## [](#%5Fonecx%5Foperator)onecx-operator

### [](#%5Finstallation)Installation

If you want to use this extension, you need to add the `org.tkit.onecx.quarkus:onecx-operator` extension first to your build file.

For instance, with Maven, add the following dependency to your POM file:

```xml
<dependency>
    <groupId>org.tkit.onecx.quarkus</groupId>
    <artifactId>onecx-operator</artifactId>
    <version>3.0.0</version>
</dependency>
```

### [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                                              | Type    | Default                  |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ------------------------ |
| [onecx.operator.touched.annotation-at](#onecx-operator%5Fonecx-operator-touched-annotation-at) Annotation name to set if resource was touched at Environment variable: ONECX\_OPERATOR\_TOUCHED\_ANNOTATION\_AT                     | string  | org.tkit.onecx.touchedAt |
| [onecx.operator.touched.annotation-by](#onecx-operator%5Fonecx-operator-touched-annotation-by) Annotation name to set if resource was touched by Environment variable: ONECX\_OPERATOR\_TOUCHED\_ANNOTATION\_BY                     | string  | org.tkit.onecx.touchedBy |
| [onecx.operator.sdk.metrics.enabled](#onecx-operator%5Fonecx-operator-sdk-metrics-enabled) Flag to enable or disable SDK metrics default: metrics are disabled (false) Environment variable: ONECX\_OPERATOR\_SDK\_METRICS\_ENABLED | boolean | false                    |
