# OneCX Local Environment

**onecx-local-env** is the local development environment for OneCX. It is based on Docker/Docker Compose, and enables developers to quickly run a local instance for development and testing purposes.

**onecx-local-env** can either be used as a standalone tool, or integrated into custom development environments via Git submodules. Custom development environments can interact with **onecx-local-env** via provided lifecycle-scripts and extend its functionality by wrapping the provided Docker Compose and script files with custom implementations.

## [](#get-and-run-onecx)Get and Run OneCX

| [Setting up](setup.html)    | Details on how to get and install OneCX locally |
| --------------------------- | ----------------------------------------------- |
| [Run OneCX](run-onecx.html) | How to start and access OneCX                   |

## [](#scripts-for-more-ease)Scripts for more Ease

Since OneCX runs in a Docker Compose environment, most settings can be managed directly through Docker and Docker Compose. However, for a more convenient approach and taking into account specific OneCX features, various shell scripts are available.

| |  Each script has the **\-h** flag to explain how to use. |
| ---------------------------------------------------------- |

The following table gives an overview of the available scripts in **onecx-local-env** root directory.  

__Table 1\. Available Scripts__
| [start-onecx.sh](scripts/start.html)                 | Start the local environment including import of inital neccessary data |
| ---------------------------------------------------- | ---------------------------------------------------------------------- |
| [stop-onecx.sh](scripts/stop.html)                   | Stop the local environment                                             |
| [import-onecx.sh](scripts/import.html)               | Import data into the local environment                                 |
| [toggle-mfes.sh](scripts/toggle-mfes.html)           | Integrate local running microfrontends directly into OneCX             |
| [check-images.sh](scripts/check-images.html)         | List local images with state and version                               |
| [update-images.sh](scripts/update-images.html)       | Update local images to the latest available versions                   |
| [list-containers.sh](scripts/list-containers.html)   | List all running containers with details and filter options            |
| [setup-truststore.sh](scripts/setup-truststore.html) | Create or update Java Truststore with custom certificates              |

## [](#additional-utilities)Additional Utilities

In addition to the OneCX Core products, further services will be launched.

__Table 2\. Available Utilities__
| [Keycloak](utilities.html#keycloak) | The IAM service used by OneCX                                                                                   |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Postgres                            | Storing the data. Each OneCX backend service has its own separate database. Access can be gained using pgAdmin. |
| [pgAdmin](utilities.html#pgadmin)   | Manage the Postgres databases.                                                                                  |
| [Traefik](utilities.html#traefik)   | Proxy service for routing requests between services within the Docker network and from/to outside.              |

## [](#onecx-applications)OneCX Applications

The OneCX Platform is a modular system which provides a lot of standard services:

Core Applications 

| Application                                             | Description                                                                                    |
| ------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| [Identity Access Management](../onecx-iam/index.html)   | Handles user authentication, authorization, and identity management within the OneCX platform. |
| [Parameter Management](../onecx-parameter/index.html)   | Used by some applications                                                                      |
| [Permission Management](../onecx-permission/index.html) | Declared and used in applications.                                                             |
| [Application Store](../onecx-product-store/index.html)  | Application data (components, slots etc.)                                                      |
| [Shell](../onecx-shell/index.html)                      | The main user interface framework for OneCX applications.                                      |
| [Tenant Management](../onecx-tenant/index.html)         | Represents a customer or organizational unit using OneCX                                       |
| [Theme Management](../onecx-theme/index.html)           | Customizing the look and feel of OneCX for a tenant                                            |
| [User Profile](../onecx-theme/index.html)               | Managing user-specific settings and preferences                                                |
| [Workspace Management](../onecx-workspace/index.html)   | Customizing the working areas for users                                                        |

Feature Applications 

| Application                                                    | Description                                                                                         |
| -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| [Announcement Management](../onecx-announcement/index.html)    | Manages announcements and notifications within the OneCX platform.                                  |
| [Bookmark Management](../onecx-bookmark/index.html)            | Bookmarks for quick access to frequently used items                                                 |
| [Data Orchestrator](../onecx-data-orchestrator/index.html)     | Manages data synchronization and integration between different OneCX services and external systems. |
| [Document Management](../onecx-document-management/index.html) | Managing documents in a user-friendly and efficient manner                                          |
| [Help Management](../onecx-help/index.html)                    | Provide users easy access to help resources and support within the portal                           |
| [Service](../onecx-service/index.html)                         | Provide various services                                                                            |
| [Test](../onecx-test/index.html)                               | Provide special functionality for testing service                                                   |
| [Welcome Management](../onecx-welcome/index.html)              | Customizing the start page for users                                                                |
