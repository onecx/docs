# Creating Import Files and Docker Compose Entry using the onecx-local-env-cli

The recommended way to set up the custom application in the OneCX environment is to use the `onecx-local-env-cli` to automate the creation of import files and the docker compose entry.

| |  This method requires a correct Helm setup for your application as it is generated with the OneCX generator. If Helm values are missing or incorrect, the CLI may not work as expected. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

To sync the app with your local environment, navigate to your hello-world UI folder and run:

```sh
npx @onecx/local-env-cli sync ui hello-world /hello-world ./helm/values.yaml -e /path/to/onecx-local-env -n hello-world-ui
```

In this command:

* `hello-world` refers to the product name.
* `/hello-world` specifies the product’s base path.
* `./helm/values.yaml` is the path to the application’s `values.yaml` file.
* `-e /path/to/onecx-local-env` should be adjusted to the path of your local `onecx-local-env` repository.
* `-n hello-world-ui` specifies the name of the microfrontend service.

This command will update your onecx-local-env with the necessary information about your new application’s UI.

To add the UI as an image to the `docker-compose.yaml` of your onecx-local-env, run (adjust the path as needed):

```sh
npx @onecx/local-env-cli docker hello-world create hello-world helloWorld -e /path/to/onecx-local-env -s ui
```

In this command: - `hello-world` after `docker` refers to the name of the custom docker compose that will be created. - `hello-world` after `create` references the product name. - `helloWorld` is the name of the UI path as defined in the `values.yaml` of the application UI. In this case it is `helloWorld` as the routing path in the `values.yaml` is `/mfe/helloWorld/`. - `-e /path/to/onecx-local-env` should be adjusted to the path of your local `onecx-local-env` repository. - `-s ui` specifies that the service to be added is the UI.

A `hello-world.docker-compose.yaml` should now be created in the onecx-local-env, containing an image for `hello-world-ui`.

| |  In the same way as for the UI we can also handle the BFF and SVC of our application by using the commands in the [General Getting Started guide](create%5Fangular%5Fapp.html#creating-the-bff). |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

For more details regarding the usage of the CLI, see the [onecx-local-env-cli README](https://github.com/onecx/onecx-local-env-cli/).

Now all necessary files are created and you can run your application in the OneCX environment as described in [Running and Testing Applications](running%5Fcustom%5Fapps%5Foverview.html#running-and-testing-applications).
