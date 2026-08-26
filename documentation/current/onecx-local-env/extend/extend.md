# Extending the OneCX default Environment

OneCX functions as a collection of microservices and microfrontends. The [OneCX Shell](../../onecx-docs-overview/architecture/shell.html) orchestrates the microfrontends for a unified user interface. This concept allows for the easy integration of other services that are launched outside the [OneCX Network](../internal/networking.html).

There are several ways to expand the OneCX local environment

## [](#integrate-a-local-running-microfrontend)Integrate a local running Microfrontend

If a microfrontend has been started separately, integration can be easily accomplished through routing and path rewriting by [Traefik](../utilities.html#traefik).

Follow the instructions [Integrate a local Microfrontend](local-mfe.html) to use your microfrontend directly in OneCX.

| |  This is the recommended procedure for integrating a **locally running microfrontend**. |
| ----------------------------------------------------------------------------------------- |

## [](#integrate-microservice-images)Integrate Microservice Images

To integrate Docker images into OneCX, you need a separate docker.compose file to manage the integration.

Follow the instructions in [Integrate Microservice Images](local-images.html) to integrate your images into OneCX.

| |  This is the recommended approach for **integrating additional microservices**.For integrating locally running microfrontends, use the method described above. |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
