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

| Application                                             | Description                                                                                                     |
| ------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| [Permission Management](../onecx-permission/index.html) | Manages permissions and access control within the OneCX platform for both the UI and BFF (Backend for Frontend) |
| [Application Store](../onecx-product-store/index.html)  | Manage Application data (components, slots, endpoints etc.)                                                     |
| [Shell](../onecx-shell/index.html)                      | The main user interface framework for OneCX applications.                                                       |
| [Theme Management](../onecx-theme/index.html)           | Customizing the look and feel of OneCX for a workspace                                                          |
| [Workspace Management](../onecx-workspace/index.html)   | Customizing the working areas for users                                                                         |

Feature Applications 

| Application                                                    | Description                                                                                                                                                                                             |
| -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Announcement Management](../onecx-announcement/index.html)    | Manages announcements assignable to workspaces and applications                                                                                                                                         |
| [Bookmark Management](../onecx-bookmark/index.html)            | Bookmarks for quick access to frequently used items                                                                                                                                                     |
| [Data Orchestrator](../onecx-data-orchestrator/index.html)     | Manages K8s Custom Resources used by the OneCX platform                                                                                                                                                 |
| [Document Management](../onecx-document-management/index.html) | Managing documents in a user-friendly and efficient manner                                                                                                                                              |
| [Help Management](../onecx-help/index.html)                    | Provide users easy access to help resources                                                                                                                                                             |
| [Identity Access Management](../onecx-iam/index.html)          | Handles user authentication, authorization, and identity management if Keycloak is used as the identity provider.                                                                                       |
| [Parameter Management](../onecx-parameter/index.html)          | Define and manage parameters used by applications                                                                                                                                                       |
| [Service](../onecx-service/index.html)                         | Provide various special services                                                                                                                                                                        |
| [Test](../onecx-test/index.html)                               | Provide special functionality for testing service                                                                                                                                                       |
| [Tenant Management](../onecx-tenant/index.html)                | Designed to handle multi-tenancy, allowing a single instance of the software to serve multiple distinct customer organizations (tenants) while keeping their data and configurations strictly isolated. |
| [User Profile](../onecx-theme/index.html)                      | Allows users to manage their personal data, preferences, and avatar images while integrating with identity management systems like Keycloak.                                                            |
| [Welcome Management](../onecx-welcome/index.html)              | It allows authorized administrators to configure the initial landing experience, including managing background images, styling options, and displaying important announcements to users upon login.     |
