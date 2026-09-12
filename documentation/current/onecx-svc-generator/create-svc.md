# Create a Backend Service

What is a Backend Service?

A Backend Service is an autonomous microservice application responsible for handling core business logic, data management, and system integrations.  
It acts as **the structural backend layer** that processes data, manages persistence, and exposes capabilities through standardized interfaces such as REST or GraphQL APIs. A backend service can function fully independently or interoperate within a larger, distributed microservices architecture, communicating with other components to deliver comprehensive business capabilities.

More details about SVC you can find in the [Quarkus SVC Guide](../docs-guides-quarkus/quarkus-svc.html).

| |  The service created with the OneCX SVC Generator contains only the base of a functional backend service.You will need to further develop and customize the application to meet your specific requirements and business logic. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#generate-the-service)Generate the Service

The **OneCX SVC Generator** creates a Quarkus-based backend service project following the standard OneCX service structure. It generates the basic project setup, application configuration, Maven build configuration, Docker and Helm files, OpenAPI skeleton, and optional GitHub Actions workflow files.

### [](#get-the-generator)Get the Generator

Overview of releases: [OneCX SVC Generator Releases](https://github.com/onecx/onecx-svc-generator/releases)

Get the Generator version v0.1.4 (examplarily)

```bash
curl -L -o onecx-svc-generator.jar \
https://github.com/onecx/onecx-svc-generator/releases/download/v0.1.4/onecx-svc-generator.jar
```

### [](#create-the-service)Create the Service

As the first step, the initial service project structure is created, and then entities are added to the project.  
The creation of a new service project takes a while.

Create the Service using the following command:

```bash
java -jar onecx-svc-generator.jar create-svc \
  --name onecx-demo-svc \
  --group org.tkit.onecx \
  --package org.tkit.onecx.demo \
  --build true
```

| |  The generator automatically uses the latest versions from GitHub for: onecx-quarkus3-parent (Maven parent POM) docker-quarkus-jvm (JVM Docker image) docker-quarkus-native (Native Docker image) helm-quarkus-app (Helm chart) If GitHub API is unavailable, well-tested default versions are used as fallback. The resolved versions are displayed during generation with source information. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#options)Options

| Option            | Description                                                                                                                                                                                                                                                                                                                                                  |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| \--name           | Specifies the generated project name of the service. The value is used also\* for the name of the generated project directory, if \--output-dir is omitted\* for Maven artifactId, if \--artifact-id is not provided\* for project-level names such as OpenAPI file names, application metadata, Helm-related project names and generated project structure. |
| \--artifact-id    | **Optional** to specify the Maven artifactId of the generated service project. This Option affects the generated Maven project configuration, but the generated project directory and OpenAPI file names remain based on \--name.If omitted, the artifact ID is derived from \--name.                                                                        |
| \--group-id       | **Optional** to specify the Maven groupId of the generated service project. The value is used in the generated Maven project configuration and generator metadata.If omitted, the group ID is org.tkit.onecx.                                                                                                                                                |
| \--package        | Specifies the base Java package name of the generated service. The value is used for generated application parts created from templates, such as controllers, DAOs, entities, mappers, services, exception mappers and tests.                                                                                                                                |
| \--output-dir     | **Optional** to specify the parent output directory where the generated service project directory will be created. The generator creates a project folder inside this directory using the value of \--name.                                                                                                                                                  |
| \--build true     | **Optional** to build the generated service project immediately after generation.If omitted, you can build it manually by running mvn clean package or mvn clean install inside the generated directory.                                                                                                                                                     |
| \--liquibase-diff | **Optional** to generate the Liquibase changelog by running the Maven db-diff profile and importing the generated diff result into the service changelog structure. If omitted, the generator creates Liquibase changelog files from its templates.                                                                                                          |

![start generating with autobuild](_images/start_generating_with_autobuild.png) 

Figure 1\. Excerpt of the build start output

![result generating with autobuild](_images/result_generating_with_autobuild.png) 

Figure 2\. Excerpt of the build result output

The generator creates a new directory (named by the value of `--name`) and sets up the basic structure for dao, controller, api and service.  
The source code is located under the base package specified by `--package`. \* `org.tkit.onecx.<package>`  
 Package name for the generated service

Next step may [create an entity schema and api components](create-schema.html).
