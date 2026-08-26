# Create Example Quarkus Project

Quarkus offers the [WEB project generator](https://code.quarkus.io/) or [Maven plugin](https://quarkus.io/guides/maven-tooling) to quickly create Quarkus project.

| |  The maven wrapper is used to specify the Maven version for the public project. Please delete the maven wrapper from the project repository. We will use the maven 3.6.2 version. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#%5Fbase%5Fproject%5Fsetup)Base project setup

But to understand the Quarkus project we will create our project from scratch. First we need to…​

Create project from template

```bash
mvn io.quarkus:quarkus-maven-plugin:{quarkus-version}:create \
    -DprojectGroupId={example-maven-group-id} \
    -DprojectArtifactId={example-maven-artifact-id} \
    -DprojectVersion={onecx-example-version} \
    -DclassName="{example-maven-class-name}" \
    -Dpath="/onecx-quarkus-example"
```

```bash
cd onecx-quarkus-example
```

| |  For all OneCX project we will have groupId=<maven-group-id>.<domain \| subdomains> and artefactId=<project-name>The project name muss be equals the git repository name. All project will use the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) and [SemVer 2.0](https://semver.org/).The maven version of the project will be 3.6.2 and it is not used to determine release artifact version. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Minimum maven configuration for our project

```xml
 <?xml version="1.0"?>
 <project xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"
         xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <modelVersion>4.0.0</modelVersion>
    <groupId>{example-maven-group-id}</groupId>
    <artifactId>{example-maven-artifact-id}</artifactId>
    <version>{maven-version}</version>
    <name>{example-maven-artifact-id}</name>
 </project>
```

### [](#%5Fparent%5Fmaven%5Fproject)Parent maven project

Pom file can be configured in many ways. The recommended way in our projects is to use **parent pom** from our repository, designed especially to use in OneCX applications. Maven parent POM (or super POM) is used to structure the project to avoid redundancies or duplicate configurations using inheritance between pom files. Maven creates a 'final POM' by merging the information from parent and module POM. In child POM we only need to include `parent`, additional dependencies that are not specified in the parent file and these dependencies that are specified in `<dependencyManagement>` section, and we want to use them. You can find more information here:

| |  More information in [Apache Maven POM Documentation](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html) |
| ---------------------------------------------------------------------------------------------------------------------------------- |

[Maven parent project source code repository](https://github.com/onecx/onecx-quarkus3-parent)

pom.xml file with parent configuration 

```xml
<?xml version="1.0"?>
 <project xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"
         xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>[[example-parent-group-id]]</groupId>
        <artifactId>[[example-maven-group-id]]</artifactId>
        <version>[[maven-version]]</version>
    </parent>

    <groupId>[[example-maven-group-id]]</groupId>
    <artifactId>[[example-maven-artifact-id]]</artifactId>
    <version>[[maven-version]]</version>
    <name>[[example-maven-artifact-id]]</name>

    <dependencies>
        <!-- project dependencies -->
    </dependencies>
 </project>
```

#### [](#%5Fdefault%5Fpom%5Fconfiguration)Default POM configuration

If you want to create pom from scratch or have better understanding how it works, you can follow undermentioned steps.

For the Quarkus application we need to add Quarkus[BOM dependencies](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html). There two possible solution:

* Quarkus BOM - this is base Quarkus which contains only Quarkus internal extensions.
* Quarkus BOM universe - this is default use with the Quarkus project generator. This BOM contains all Quarkus extension and external project like [Quarkus Camel extension](https://github.com/apache/camel-quarkus).

Example of the parent pom configuration 

```xml
<properties>
    <!-- build -->
    <format.skip>false</format.skip>
    <enforcer.skip>false</enforcer.skip>
    <enforce-test-deps-scope.skip>${enforcer.skip}</enforce-test-deps-scope.skip>
    <!-- Quarkus configuration -->
    <quarkus.version>3.13.2</quarkus.version>
    <quarkus.smallrye-open-api.version>3.1.1</quarkus.smallrye-open-api.version>
    <quarkiverse.quarkus-openapi-generator.version>1.3.1</quarkiverse.quarkus-openapi-generator.version>
    <quarkiverse.mockserver.version>0.6.0</quarkiverse.mockserver.version>
    <!-- tkit -->
    <tkit.quarkus.version>2.31.0</tkit.quarkus.version>
    <!-- Maven configuration -->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
    <maven.compiler.release>17</maven.compiler.release>
    <maven.compiler.parameters>true</maven.compiler.parameters>
    <maven.compiler-plugin.version>3.10.1</maven.compiler-plugin.version>
    <maven.surefire-plugin.version>3.0.0</maven.surefire-plugin.version>
    <maven.formatter-plugin.version>2.22.0</maven.formatter-plugin.version>
    <maven.impsort-plugin.version>1.8.0</maven.impsort-plugin.version>
    <maven.enforcer-plugin.version>3.2.1</maven.enforcer-plugin.version>
    <!-- Maven central release configuration -->
    <nexus.staging-plugin.version>1.6.13</nexus.staging-plugin.version>
    <source-plugin.version>3.2.1</source-plugin.version>
    <javadoc-plugin.version>3.5.0</javadoc-plugin.version>
    <gpg-plugin.version>3.0.1</gpg-plugin.version>
    <!-- Sonar -->
    <sonar.coverage.exclusions>
        **/model*/**/*.*,**/resources/**/*.*,**/JaxRsActivator*
    </sonar.coverage.exclusions>
<!--        <sonar.exclusions></sonar.exclusions>-->

    <!-- Other -->
    <projectlombok.version>1.18.26</projectlombok.version>
    <projectlombok.mapstruct-binding.version>0.2.0</projectlombok.mapstruct-binding.version>
    <mapstruct.version>1.5.5.Final</mapstruct.version>
    <assertj.version>3.24.2</assertj.version>
    <hibernate-orm.version>5.4.27.SP1</hibernate-orm.version>
</properties>
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-bom</artifactId>
            <version>3.13.2</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
        <dependency>
            <groupId>org.tkit.quarkus.lib</groupId>
            <artifactId>tkit-quarkus-bom</artifactId>
            <version>4.6.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

We also set up the project for java `17` version and source code encoding to `UTF-8`.

#### [](#%5Fcompiler)Compiler

Now we would need to add the Maven plugins to build the Quarkus application correctly.

* maven-compile-plugin - execute java compilation process
* quarkus-maven-plugin - extends the compilation process to generated Quarkus byte-code and add the development mode for maven project.

Configuration of the Quarkus maven plugin 

```xml
    
        
            io.quarkus
            quarkus-maven-plugin
            {quarkus-version}
            true
                
                    
                        build
                        generate-code
                        generate-code-tests
                    
                        
                            true
                            localhost
        
        
            org.apache.maven.plugins
            maven-compiler-plugin
            
                
                    -parameters
                    -Amapstruct.defaultComponentModel=cdi
                    -Amapstruct.defaultInjectionStrategy=constructor
                
                    
                        org.mapstruct
                        mapstruct-processor
                        ${mapstruct.version}
                    
                    
                        org.projectlombok
                        lombok
                        ${projectlombok.version}
                    
                    
                        org.projectlombok
                        lombok-mapstruct-binding
                        ${projectlombok.mapstruct-binding.version}
                    
                    
                        org.hibernate
                        hibernate-jpamodelgen
                        ${hibernate-orm.version}
    

```

The configuration for the <http://maven.apache> org/plugins/maven-compiler-plugin/compile-mojo.html\[maven-compile-plugin\] `parameters`is set to `true` to generate metadata for reflection on method parameters.

### [](#%5Fcompilation)Compilation

Now we can compile our project:

```bash
mvn clean package
```

All the quarkus project are microservices where we push docker image and helm chart to registry. The maven `install` does not need to be executed.
