# Creating a OneCX Application

This guide walks you through the process of creating a simple OneCX Application using the [OneCX App Generator](../onecx-nx-plugins/index.html) and integrating it into your local OneCX environment.

## [](#introduction)Introduction

What is a OneCX Application?

A OneCX Application is a set of microfrontends and services that together provide specific functionality within the OneCX platform. It typically consists of a user interface (a microfrontend) and backend services that support its operations. A OneCX Application is designed to be modular, scalable, and easily integrable with other applications within the OneCX ecosystem.

See also:

* [OneCX Application Concept](../onecx-docs-overview/architecture/index.html#applications) provides more information about the concept of OneCX Applications.
* [OneCX Application List](../onecx-docs-apps/index.html) for a list of existing OneCX Applications with details.

A OneCX Application consists typically of the following components.

Application Components (examplarily for the Hello World app)

* **onecx-hello-world-ui** ⇒ Microfrontend  
The user interface (UI) component that displays the welcome message.
* **onecx-hello-world-bff** ⇒ Microservice  
Backend For Frontend (BFF) service that handles any backend logic required by the UI.
* **onecx-hello-world-svc** ⇒ Microservice  
Backend Service (SVC): A simple service that could be used to log visits to the application (optional for this basic example).

In some cases it consists only of a microfrontend without any backend services or only backend services without a UI component.

## [](#prerequisites)Prerequisites

Before you begin, ensure you have the following prerequisites in place:

* A working OneCX Local Environment set up. If you haven’t done this yet, follow the instructions in the [OneCX Local Environment Setup](../onecx-local-env/setup.html).
* Node.js, npm, nx installed on your development machine.
* Familiarity with [Angular](https://angular.de/) or [React](https://reactjs.org/), as the microfrontends in OneCX are typically built using these frameworks.
* You need about 1GB of free disk space and it may take a few minutes to download and set up all necessary dependencies.

## [](#create-the-ui-component)Create the UI Component

In this tutorial, we will create a simple OneCX application with [Angular](https://angular.de/) called "Hello World" that displays a welcome message to users.

### [](#generate-ui-component)Generate UI Component

First, we will generate the **onecx-hello-world-ui** using the OneCX App Generator.

1. Open a terminal and navigate to the directory where you want to create your OneCX Application.
2. Run the OneCX App Generator command:  
Create a new UI component using the ngrx template:  
```bash  
npx @onecx/create-workspace ngrx onecx-hello-world-ui  
```
3. Follow the prompts to provide details about your app, such as its name, description, and any specific configurations you want to include.
4. Once the generation process is complete, navigate into your new `onecx-hello-world-ui` directory and update dependencies:  
```bash  
cd onecx-hello-world-ui  
npm install  
```

### [](#fixing-ui-component)Fixing UI Component

The generated **onecx-hello-world-ui** component requires a few adjustments to align with our naming conventions and to ensure proper integration with the backend services.

1. Renaming and fixing OpenAPI file:  
   * Navigate to the `src/assets/swagger/` folder inside the **onecx-hello-world-ui** project.  
   * Rename the directory `swagger` to `api`.  
   * Rename the file `onecx-hello-world-ui-bff.yaml` to `openapi-bff.yaml`.  
   * Open the file and replace all occurrences of `onecx-hello-world-ui-bff` with `onecx-hello-world-bff`.  
   * Save the changes  
   * Navigate back to the `root` folder of the **onecx-hello-world-ui** project.  
   * Open the file `package.json` and replace all occurrences of `src/assets/swagger/onecx-hello-world-bff.yaml` with `src/assets/api/openapi-bff.yaml`.  
   * Save the changes
2. Generate the API client code based on the updated OpenAPI specification:  
Generate the API client code:  
```bash  
npm run apigen  
```
3. Fixing Docker file:  
   * Open the `Dockerfile` located in the root of the **onecx-hello-world-ui** project.  
   * Locate the line that sets the `BFF_URL` environment variable.  
   * Change the value from `<http://onecx-hello-world-ui-bff:8080/>` to `<http://onecx-hello-world-bff:8080/>`.  
   * Save the changes.
4. Fixing Proxy configuration:  
   * Open the `proxy.conf.js` file located in the root of the **onecx-hello-world-ui** project.  
   * Locate the `target` property under the `/bff` proxy configuration.  
   * Change the value from `<http://onecx-hello-world-ui-bff>` to `<http://onecx-hello-world-bff>`.  
   * Save the changes.
5. Fixing the **app name** throughout the project:  
   1. In the Webpack configuration:  
         * Open the `webpack.config.js` file located in the root of the **onecx-hello-world-ui** project.  
         * Locate the `name` property in the `ModuleFederationPlugin` configuration.  
         * Change the value from `onecx-hello-world-ui-app` to `onecx-hello-world-ui`.  
         * Save the changes.  
   2. In the Typescript configuration:  
         * Open the `tsconfig.app.json` file located in the root of the **onecx-hello-world-ui** project.  
         * Locate the line with `.remote-module` property within the `files` section.  
         * Change the value from `onecx-hello-world-ui-app.remote.module.ts` to `onecx-hello-world-ui.remote.module.ts`.  
         * Save the changes.  
   3. In the Bootstrap configuration:  
         * Open the `bootstrap.ts` file located in the `src` of the **onecx-hello-world-ui** project.  
         * Locate the line with import the UI module.  
         * Change the value from `onecx-hello-world-ui-app.remote.module.ts` to `onecx-hello-world-ui.remote.module.ts`.  
         * Save the changes.  
   4. In the App module configuration:  
         * Open the `app.module.ts` file located in the `src/app` of the **onecx-hello-world-ui** project.  
         * Locate the line with imports the `PortalCoreModule`.  
         * Change the value from `onecx-hello-world-ui-app` to `onecx-hello-world-ui`.  
         * Save the changes.  
   5. Change the remote module file name:  
         * Rename the file `onecx-hello-world-ui-app.remote.module.ts` to `onecx-hello-world-ui.remote.module.ts` in the `src/app` of the **onecx-hello-world-ui** project.
6. Fixing the **module name** inside the remote module file:  
   1. Open the `onecx-hello-world-ui.remote.module.ts` file located in the `src/app` of the **onecx-hello-world-ui** project.  
         * Locate the `export class` declaration.  
         * Change the value from `OnecxHelloWorldUiModule` to `OneCXHelloWorldModule`.  
         * Save the changes.  
   2. In the Bootstrap configuration:  
         * Open the `bootstrap.ts` file located in the `src` of the **onecx-hello-world-ui** project.  
         * Locate the 2 affected lines where the module is referenced.  
         * Change the value from `OnecxHelloWorldUiModule` to `OneCXHelloWorldModule`.  
         * Save the changes.  
   3. In the Webpack configuration:  
         * Open the `webpack.config.js` file located in the root of the **onecx-hello-world-ui** project.  
         * Locate the exposed module name  
         * Change the value from `OnecxHelloWorldUiModule` to `OneCXHelloWorldModule`.  
         * Save the changes.  
   4. In the values.yaml:  
         * Open the `values.yaml` file located in the `helm` directory of the **onecx-hello-world-ui** project.  
         * Locate the exposed module name  
         * Change the value from `OnecxHelloWorldUiModule` to `OneCXHelloWorldModule`.  
         * Save the changes.  
   5. Change the **app title**:  
         * Open the `index.html` file located in the `src` of the **onecx-hello-world-ui** project.  
         * Locate the `<title>` tag.  
         * Change the value from **OnecxHelloWorldUi App UI** to **OneCX Hello World UI**.  
         * Save the changes.
7. Fixing the **routing path** :  
   * Open the `values.yaml` file located in the `helm` directory of the **onecx-hello-world-ui** project.  
   * Locate the `path` property under the `routing` configuration.  
   * Change the value from `/mfe/onecxHelloWorldUi/` to `/mfe/helloworld/`.  
   * Save the changes.

Your **onecx-hello-world-ui** component is now set up.

### [](#testing-ui-component)Testing UI Component

After developing your UI component, it’s important to test it locally to ensure everything works as expected before deploying it within your OneCX environment.

Start the UI component locally with:

```bash
nx serve onecx-hello-world-ui --proxy-config=proxy.conf.js
```

Now you can see the UI works with accessing the remoteEntry.js via `<http://localhost:4200/remoteEntry.js>`.

or alternatively,

Use the start script and a custom port:

```bash
npm run start -- --port=6021 --host 0.0.0.0 --disableHostCheck --publicHost=http://localhost:6021
```

This will start the UI component on port 6021, and you can access it at `<http://localhost:6021/remoteEntry.js>`.

![screenshot successful start local mfe](_images/screenshot_successful-start-local-mfe.png) 

Figure 1\. Successfully running UI component on port 6021
