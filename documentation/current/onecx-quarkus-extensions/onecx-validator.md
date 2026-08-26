# undefined

## [](#%5Fonecx%5Fvalidator)onecx-validator

### [](#%5Finstallation)Installation

If you want to use this extension, you need to add the `org.tkit.onecx.quarkus:onecx-validator` extension first to your build file.

For instance, with Maven, add the following dependency to your POM file:

```xml
<dependency>
    <groupId>org.tkit.onecx.quarkus</groupId>
    <artifactId>onecx-validator</artifactId>
    <version>3.0.0</version>
</dependency>
```

### [](#%5Fusage)Usage

#### [](#%5Fconstraints)Constraints

| |  Constraints are generated automatically from the open-api definition file. See [Constraints](onecx-openapi-generator.html#%5Fconstraints) |
| -------------------------------------------------------------------------------------------------------------------------------------------- |

##### [](#%5Fsize)@Size

`@org.tkit.onecx.quarkus.validator.constraints.Size` constraints annotation validate the numeric value between min and max attribute. Additional to these constraints contain parameter key which cloud be optionally mapped to the [onecx-parameters](onecx-parameters.html) backend service and this enables dynamic validation of the parameter.

### [](#%5Fconfiguration)Configuration

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                                                                                                                                                                         | Type               | Default                                             |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ | --------------------------------------------------- |
| [onecx.validator.values.enabled](#onecx-validator%5Fonecx-validator-values-enabled) Whether parameter-svc is enabled in case the parameter extension is present. Environment variable: ONECX\_VALIDATOR\_VALUES\_ENABLED                                                                                                                                       | boolean            | true                                                |
| [onecx.validator.values.mapping."mapping"](#onecx-validator%5Fonecx-validator-values-mapping-mapping) Key to parameter-name mapping Environment variable: ONECX\_VALIDATOR\_VALUES\_MAPPING\_\_MAPPING\_                                                                                                                                                       | Map<String,String> |                                                     |
| [onecx.validator.size.template](#onecx-validator%5Fonecx-validator-size-template) Template for the constraint violations error message 6 parameters required: %1$s, %2$s, %3$s, %4$s, %5$d, %6$d %1$s = provider %2$s = key %3$s = parameter %4$s = message %5$d = min-size value %6$d = max-size value Environment variable: ONECX\_VALIDATOR\_SIZE\_TEMPLATE | string             | Parameter: %3$s Boundaries: %5$d Bytes - %6$d Bytes |
