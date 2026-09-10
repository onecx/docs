# Create a React UI App

What is a UI App?

Unresolved include directive in modules/onecx-nx-plugins/pages/react/create-app.adoc - include::../partials/\_glossary.adoc\[\]

| |  The UI App created with the OneCX App Generator is only the base of a functional UI application. You will need to further develop and customize the application to meet your specific requirements and business logic. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#generate-a-react-ui-app)Generate a React UI App

The React generator supports different templates and configurations. The creation of a new workspace takes a while, as the generator sets up a complete React application with all necessary dependencies and configurations.

Generate the React UI App with following commands

```bash
npx <namespace>/create-workspace react <product>
cd <product>
npm install
----
```

with:

| _<namespace>_ | The base namespace of the project where the application is part of.For the OneCX, use @onecx.                                          |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| _<flavor>_    | ngrx (or angular).                                                                                                                     |
| _<product>_   | The technical base name of the application (product) for a certain business case.E.g. bookstore for an application named "Book Store". |

The generator creates a new directory with the specified product name and sets up the OneCX React UI App according to the chosen template. Please note that the product name from your command is used as base of some essential application parts as following:

### [](#key-naming-conventions)Key Naming Conventions

* `onecx-<product>-ui`  
Project name  
Remote name for module federation  
Helm chart name for deployment and microservice registration in OneCX
* `OneCX<product>Module`  
Module name
* `ocx-<product>-component`  
Tag name for integration the web component into the DOM
* `onecx-apps/onecx-<product>-ui`  
Repository name for docker image repository
* `/mfe/<product>/`  
Base path for the microfrontend application, used within OneCX for integration purposes

Next step may [create a feature module](create-feature.html).

| |  The generated app contains the dependency for the OneCX React Generator (@onecx/react-generator).This allows you to easily add new features, components, and services within your app’s user interface using the OneCX React Generator functions. |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Unresolved include directive in modules/onecx-nx-plugins/pages/react/create-app.adoc - include::\_integrate-into-onecx.adoc\[\]

## [](#example)Example

The following commands create a new workspace directory named "bookstore" with the necessary structure and configurations for a OneCX React UI App. The generator sets up a complete [React](https://reactjs.org/) application with all necessary dependencies and configurations.

Create a UI App named "bookstore" (product)

```bash
npx @onecx/create-workspace react bookstore
cd bookstore
npm install
```
