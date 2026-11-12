# Create a UI App

What is a UI App?

A UI App is a microfrontend application built using modern web technologies such as [Angular](https://angular.de/) or [React](https://reactjs.org/). Such application is designed to seamlessly integrate with the OneCX platform, providing a consistent user experience across different modules and features.  
Within the OneCX ecosystem, a UI App typically serves as the **front-end interface** for users to interact with various functionalities offered by OneCX. It can be a standalone application or part of a larger suite of applications, and it communicates with backend services to fetch and display data, handle user inputs, and perform various operations.

| |  The UI App created with the OneCX App Generator is only the base of a functional UI application. You will need to further develop and customize the application to meet your specific requirements and business logic. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#generate-a-ui-app)Generate a UI App

The Angular generator supports three flavors: **angular**, **ngrx** and **standalone-ngrx** (with the OneCX standalone development shell).  
It is **recommended to use the NgRx** flavor, because it leads to better structured projects and the state management is already in place.  
The creation of a new workspace takes a while, as the generator sets up a complete Angular application with all necessary dependencies and configurations.

Generate the UI App with following commands

```bash
npx <namespace>/create-workspace <flavor> <product> [--appPrefix=<prefix>]
cd <product>
npm install
```

with:

| _<namespace>_  | The base namespace of the project where the application is part of.For the OneCX, use @onecx.                                                                                                                         |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _<flavor>_     | angular, ngrx, standalone-ngrx or react.                                                                                                                                                                              |
| _<product>_    | The technical base name of the application (product) for a certain business case.E.g. bookstore for an application named "Book Store".                                                                                |
| _\--appPrefix_ | Optional application prefix, default empty. Use \--appPrefix=onecx for legacy application naming, \--appPrefix=acme for a custom prefix, or\--appPrefix="" for explicitly empty. Do not include a trailing separator. |

The generator creates a new directory with the specified product name and sets up the OneCX UI App according to the chosen flavor.  
Please note that the product name from your command is used as base of some essential application parts as following:

### [](#key-naming-conventions)Key Naming Conventions

`appPrefix` is optional and defaults to the empty string. Use `--appPrefix=onecx` to retain the legacy application prefix, `--appPrefix=acme`for a custom prefix, or `--appPrefix=""` for an explicitly empty prefix. The separated forms `--appPrefix acme` and `--appPrefix ""` also work. Prefixes are lowercase kebab-case with no trailing separator. For product `orders`, omitted/empty yields `orders-ui` and `orders-bff`;`onecx` yields `onecx-orders-ui` and `onecx-orders-bff`;`acme` yields `acme-orders-ui` and `acme-orders-bff`.

The prefix is applied once to the product slug. It does not change the workspace directory, product-based routes or OneCX framework dependencies. For an example with `--appPrefix=acme` and product `orders`:

* `acme-orders-ui`  
Project name  
Helm chart name for deployment and microservice registration in OneCX
* `acmeOrdersUi`  
Identifier-safe federation remote name (also used in operator metadata)
* `AcmeOrdersUiModule` / `./AcmeOrdersUiModule`  
Module class and federation exposed identifier, imported from `acme-orders-ui.remote.module.ts`
* `acme-orders-ui-component`  
Tag name for integration the web component into the DOM
* `onecx-apps/acme-orders-ui`  
Repository name for docker image repository
* `/mfe/<product>/`  
Base path for the microfrontend application, used within OneCX for integration purposes
* `dist/acme-orders-ui/`  
Build output and Docker COPY source
* `<http://acme-orders-bff:8080/>`  
Default Docker, development proxy and OpenAPI BFF destination

The same option works directly on the generators, for example:

```bash
nx g @onecx/angular-generator:ngrx orders --appPrefix=acme --non-interactive
```

Next step may [create a feature module](create-feature.html).

| |  The generated app contains the dependency for the OneCX Angular Generator (@onecx/angular-generator).This allows you to easily add new features, components, and services within your app’s user interface using the OneCX Angular Generator functions.(This package was named @onecx/nx-plugin prior to version 9.) |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#integrate-ui-app-into-onecx)Integrate UI App into OneCX

After the generation, you need to integrate the generated App into the local running OneCX. This involves adding the search component to the routing configuration of the feature module and ensuring that it is properly linked to the rest of the application.

| |  It is recommended to use the mechanism of OneCX Local environment to integrate the generated UI App into the running OneCX environment. Follow the guide in [Extend OneCX](../../onecx-local-env/extend/extend.html). |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

Steps for integration:

* Start the application with a dedicated port  
```bash  
npm run start -- --port=6023 --publicHost=http://localhost:6023  
```
* Integrate the application into running OneCX environment with this port  
```bash  
./toggle-mfes.sh -a bookstore:6023  
```
* Add necessary data to the backend to be able to call the search component  
(product, permissions, workspace registration, menu entry, etc.)
* After making these changes, reload the OneCX UI and navigate to the search component route

## [](#example)Example

The following commands create a new workspace directory named "bookstore" with the necessary structure and configurations for a OneCX UI App using [NgRx](https://ngrx.io/). This can take a while, as the generator sets up a complete [Angular](https://angular.de/) application with all necessary dependencies and configurations.

Create a UI App named "bookstore" (product) with NgRx support

```bash
npx @onecx/create-workspace ngrx bookstore
cd bookstore
npm install
```

![generated workspace bookstore](../_images/generated_workspace_bookstore.png) 

Figure 1\. Illustrative workspace layout (application filenames follow the naming conventions above)
