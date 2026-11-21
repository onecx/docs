# Add an Application Manually to OneCX

When you have created a custom application and want to run it in the OneCX local environment, you need to add the application to the OneCX. This involves adding the application to the product store, adding the application to the workspace, and assigning permissions and roles for accessing the application.

This guide is created for webpack module apps. To see all supported types of microservices, see the [Microservices and Microfrontends](../../../onecx-docs-overview/architecture/microservices.html) documentation.

Alternatively you can use `local-env-cli` to add your application to the OneCX local environment. See [local-env-cli](../../../onecx-docs-start/first-app/app%5Fsetup%5Fcli.html) for more details.

## [](#prerequisites)Prerequisites

Before you can add your custom application to the OneCX, you need to have the following prerequisites in place:

* Your UI app needs to have webpack module federation implemented. See the [Module Federation with Webpack](../../../onecx-docs-overview/module-federation/webpack.html) documentation for details on how to implement webpack module federation in your application.
* You have to add the [micro frontend](../local-mfe.html) to the OneCX local environment using `./toggle-mfe` script.

## [](#guide-steps)Guide Steps

1. [Add the application to the Application Store](add%5Fappl%5Fto%5Fproduct%5Fstore.html)
2. [Register the application in the Workspace](add%5Fappl%5Fto%5Fworkspace.html)
3. [Assign permissions and roles (Optional)](add%5Fpermissions.html)

| |  Like all manual changes in the local environment, manually created applications will be lost when the Postgres volume is deleted (e.g. by running ./stop-onecx.sh -c). |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
