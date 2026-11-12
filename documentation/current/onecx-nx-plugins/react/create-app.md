# Create a React UI App

What is a UI App?

Unresolved include directive in modules/onecx-nx-plugins/pages/react/create-app.adoc - include::../partials/\_glossary.adoc\[\]

| |  The UI App created with the OneCX App Generator is only the base of a functional UI application. You will need to further develop and customize the application to meet your specific requirements and business logic. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#generate-a-react-ui-app)Generate a React UI App

The React generator supports different templates and configurations. The creation of a new workspace takes a while, as the generator sets up a complete React application with all necessary dependencies and configurations.

Generate the React UI App with following commands

```bash
npx <namespace>/create-workspace react <product> [--appPrefix=<prefix>]
cd <product>
npm install
```

with:

| _<namespace>_  | The base namespace of the project where the application is part of.For the OneCX, use @onecx.                                                                                                                         |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _<flavor>_     | angular, ngrx, standalone-ngrx or react.                                                                                                                                                                              |
| _<product>_    | The technical base name of the application (product) for a certain business case.E.g. bookstore for an application named "Book Store".                                                                                |
| _\--appPrefix_ | Optional application prefix, default empty. Use \--appPrefix=onecx for legacy application naming, \--appPrefix=acme for a custom prefix, or\--appPrefix="" for explicitly empty. Do not include a trailing separator. |

The generator creates a new directory with the specified product name and sets up the OneCX React UI App according to the chosen template. Please note that the product name from your command is used as base of some essential application parts as following:

### [](#key-naming-conventions)Key Naming Conventions

`appPrefix` defaults to the empty string. Use `--appPrefix=onecx` for legacy application naming, `--appPrefix=acme` for custom naming, or `--appPrefix=""`for an explicitly empty prefix. Separated forms (`--appPrefix acme`,`--appPrefix ""`) also work. Prefixes are lowercase kebab-case without a trailing separator. For `orders`, omitted/empty produces `orders-ui` and `orders-bff`;`onecx` produces `onecx-orders-ui` and `onecx-orders-bff`;`acme` produces `acme-orders-ui` and `acme-orders-bff`.

For product `orders` with `--appPrefix=acme`:

* `acme-orders-ui`  
Project name  
Helm chart name for deployment and microservice registration in OneCX
* `acmeOrdersUi`  
Identifier-safe federation remote name, matching operator metadata
* `./AcmeOrdersUiModule`  
Federation exposed identifier pointing to `src/bootstrap.ts`
* `acme-orders-ui-component`  
Tag name for integration the web component into the DOM
* `onecx-apps/acme-orders-ui`  
Repository name for docker image repository
* `dist/acme-orders-ui/`  
Build output and Docker COPY source
* `<http://acme-orders-bff:8080/>`  
Default Docker, development proxy (`/bff`) and OpenAPI BFF destination
* `onecx-<product>` / `/onecx-<product>` / `/mfe/onecx-<product>/`  
Existing product registration, product base path and asset base are unchanged, independent of application prefix.

Workspace directories and OneCX framework packages/APIs are unchanged.

Direct generator usage also supports the option:

```bash
nx g @onecx/react-generator:react orders --appPrefix=acme --non-interactive
```

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
