# Running Custom Applications in OneCX

After [creating a new application](create%5Fangular%5Fapp.html), we want to run it in our local environment. This guide walks you through the process of setting up, running, testing, and removing custom applications in the OneCX environment. It covers different ways to achieve these tasks using a custom "Hello World" application as an example.

Before you begin, please ensure your local OneCX environment is already set up and running correctly. For setup instructions, refer to the [onecx-local-env documentation](../../onecx-local-env/index.html). Additionally, make sure that entries for `hello-world-bff` and `hello-world-svc` are added to your system’s hosts file (`C:\Windows\System32\drivers\etc\hosts` on Windows) the same way as it was done in the [onecx-local-env setup](../../onecx-local-env/setup.html).

## [](#application-setup)1\. Application Setup

We first need to define our application, microservice, Ui Component and register the application in our workspace. There are two main approaches to add the necessary data. You can either create the import files and update the container definitions manually, or you can use the `onecx-local-env-cli` to automate the process. The recommended method depends on how your application was created:

* If you used the OneCX generator as outlined in the [Getting Started guide](create%5Fangular%5Fapp.html), you can quickly set up your application using the `onecx-local-env-cli`. See the detailed steps here: [Application Setup using OneCX CLI](app%5Fsetup%5Fcli.html)
* If your application was created manually or lacks the Helm structure provided by the OneCX generator, you can also manually create the setup in the `onecx-local-env`: [Manual Application Setup](app%5Fsetup%5Fmanual.html).

## [](#running-and-testing-applications)2\. Running and Testing Applications

After the necessary import and docker files were created as explained in step 1, you can run and test the application in the OneCX Shell in one of the following ways.

* You can use Docker’s build context to build the image from your local application each time you run Docker Compose. With the build context specified in `docker-compose.yaml`, Docker will automatically build the image from the local Dockerfile of your application: [Automatic Image Build](image%5Fbuild%5Fautomatic.html)
* You can also manually build the Docker image from your local application and use this local image in your `onecx-local-env`. This method avoids potential caching issues that may arise when using the automatic image build: [Manual Image Build](image%5Fbuild%5Fmanual.html)

## [](#local-applications)3\. Local Applications

In addition to the methods mentioned above, you can configure your application for hot reloading to speed up development and testing.

* If you want to your application to reflect changes immediately without rebuilding the image each time and only starting the application once, you can set up your application for hot reloading: [Hot Reload](enable%5Fhot%5Freload.html)
* You can also run and test multiple local applications simultaneously: [Multiple Applications](run%5Fmultiple%5Fapps.html)

## [](#testing-changes-to-existing-onecx-core-apps)4\. Testing Changes to Existing OneCX Core Apps

You can also test changes to existing OneCX core applications in your local OneCX environment: [Testing Core Apps](testing%5Fexisting%5Fcore%5Fapps.html)

## [](#removal-of-custom-app)5\. Removal of Custom App

If you need to remove a custom app from the environment, you can do so by following the steps outlined in [Removal of Custom App](app%5Fremoval.html).
