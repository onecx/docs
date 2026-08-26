# Quarkus in OneCX

This guide provides best practices and guidelines for developing microservices using Quarkus within the OneCX platform. It covers project structure, REST API design, backend for frontends (BFF) patterns, backend services, and Kubernetes operator integration.

Quarkus Kubernetes native Java stack comes with an extendable framework.

* Homepage: <https://quarkus.io/>
* Guides: <https://quarkus.io/guides/>
* Source code: <https://github.com/quarkusio/quarkus>
* Quarkus quick starts: <https://github.com/quarkusio/quarkus-quickstarts>
* Quarkiverse: <https://quarkiverse.github.io/quarkiverse-docs/index/index/index.html>
* Quarkiverse source code: <https://github.com/quarkiverse>
* [1000kit Quarkus Extensions](https://1000kit.github.io/tkit-quarkus/current/tkit-quarkus/index.html)
* [API Guidelines](../onecx-docs-dev/guidelines/api%5Fguidelines.html)

## [](#%5Ftools)Tools

For the developing the Quarkus application we need to install these tools:

* [IntelliJ IDEA](https://www.jetbrains.com/de-de/idea/download/) **RECOMMENDED!**  
   * Plugins  
         * Quarkus Tools by Red-Hat  
         * Lombok  
         * Zalando OpenAPI Editor  
         * SonarLint (disable Automatically trigger analysis)  
   * Maven  
         * Use Maven installation from your WSL `\\wsl.localhost....`  
   * JDK  
         * Use JDK installation from your WSL `\\wsl.localhost....`
* [Visual Code](https://code.visualstudio.com/download)
* [NeoVim](https://neovim.io/)

## [](#%5Fuseful%5Fresources)Useful Resources

* [Quarkus workshop](https://quarkus.io/quarkus-workshops/super-heroes/)
* [MicroProfile - specification](https://microprofile.io/)
* [Smallrye - MicroProfile implementation](https://smallrye.io/)
* [Java tutorial](https://docs.oracle.com/javase/tutorial/)
* [TestContainers](https://www.testcontainers.org/)
* [Kubernetes](https://kubernetes.io/)
* [Docker](https://www.docker.com/)
