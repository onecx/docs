# Scripts for more Ease

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
