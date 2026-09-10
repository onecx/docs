# React Generators

In addition to the Angular generators, the OneCX App Generator provides generators for **React** UI applications. They follow the same iterative approach: generate a part, then adapt the places marked with **ACTION**.

## [](#quickstart-generate-an-app)Quickstart: Generate an app

Requirements: Node, Nx, and the plugin installed locally.

1. Build the workspace and the generator:

npm install
npm run build

1. Generate a sample app (example):

npx nx g @onecx/react-generator:react my-sample-app

1. Inspect generated Helm snippet at `helm/values.yaml` in the generated project.

Example generated snippet:

product:
  info:
    name: MySampleApp
app:
  operator:
    microfrontend:
      specs:
        - exposedModule: './OneCXMySampleAppModule'
          shareScope: 'react_19'
          remoteName: 'ocx-my-sample-app'
          tagName: 'ocx-my-sample-app-entrypoint'
          type: MODULE
    microservice:
      spec:
        type: ui

See the Shared Generator Guide for conventions and template variables: [Shared Generator Guide](#../generator/shared-generator-guide.adoc)

The current working directory must be the root of an existing OneCX React UI Application.

## [](#available-generators)Available Generators

* [Create a React Feature Module](create-feature.html)  
Generates a feature entry page and registers feature-level routing.
* [Create a React Detail Component](create-details.html)  
Generates details page, hook/store, and related UI components for a resource.
* [Create a React Search Page](create-search.html)  
A data-driven search page with criteria, results table, header actions and API integration.
* [Create a React Page](create-page.html)  
A minimal, ready-to-use page with header and content area.
