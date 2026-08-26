# K8s operator (operator)

## [](#%5Fproject%5Fsetup)Project setup

Now that [project structure](project-structure.html) is set up for the Onecx Quarkus project, we can configure the k8s operator and extend the project configuration.

### [](#%5Fparent%5Fconfiguration)Parent configuration

Project maven parent configuration, artifactId and project version.

| |  More information about maven parent pom pattern [Apache Maven Pom Documentation](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html) |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Maven parent configuration 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>org.tkit.onecx</groupId>
        <artifactId>onecx-quarkus3-parent</artifactId>
        <version>0.62.0</version>
    </parent>

    <artifactId>onecx-example-svc</artifactId>
    <version>999-SNAPSHOT</version>

</project>
```
