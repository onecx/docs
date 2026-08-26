# OneCX Quarkus Extensions

## [](#%5Finstallation)Installation

Include the following bom artifact into your pom or parent pom and then pick the components you need.

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.tkit.onecx.quarkus</groupId>
            <artifactId>onecx-quarkus-bom</artifactId>
            <version>3.0.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

| |  Some component come with additional documentation and configuration - check the 'Documentation' link for particular section. |
| ------------------------------------------------------------------------------------------------------------------------------- |

## [](#%5Fcomponents)Components

Include the component in your project by including the corresponding dependency.

* [Onecx Core](onecx-core.html)
* [Onecx Permissions](onecx-permissions.html)
* [Onecx Tenant](onecx-tenant.html)
* [Onecx Parameters](onecx-parameters.html)
* [Onecx OpenApi Generator](onecx-openapi-generator.html)
* [Onecx Validator](onecx-validator.html)
* [Onecx Operator](onecx-operator.html)
