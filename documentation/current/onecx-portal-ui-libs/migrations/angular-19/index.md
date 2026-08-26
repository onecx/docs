# Migrate OneCX App from Angular 18 to Angular 19

## [](#overview)Overview

This guide provides comprehensive step-by-step instructions for migrating OneCX applications from Angular 18 to Angular 19\. As part of upgrading to Angular 19, you must update your OneCX UI libraries to version 6\. This library update is not a standalone migration but a required part of the Angular version upgrade process, as OneCX v6 libraries provide Angular 19 compatibility and include necessary breaking changes.

## [](#prerequisites)Prerequisites

Before starting this migration:

* Your OneCX application is currently running on Angular 18
* You have OneCX UI libraries v5.x installed
* You have a working development environment

## [](#ai-driven-migration-assistance)AI Driven Migration Assistance

To simplify the migration process, you can use the AI-driven migration assistant. The [OneCX AI Refactoring Agents](https://github.com/onecx/onecx-ai-refactoring-agents) repository provides a dedicated migration agent to automate the OneCX Angular migration process. Below is the migration agent setup, which you can copy and use with your preferred AI tool. These agents have been tested with GitHub Copilot (Claude Sonnet 4.6) in agent mode.

AI Migration Agent 

**Before You Start**

Make sure you have the Recommended MCP servers configured before running the migration agent. For detailed setup instructions, see the [MCP Server Setup Guide](../../../onecx-docs-dev/ai/mcp%5Fserver%5Fsetup.html).

**Setup**

1. Clone or pull the latest version of the repository:  
```bash  
git clone https://github.com/onecx/onecx-ai-refactoring-agents.git  
# or if already cloned:  
cd onecx-ai-refactoring-agents && git pull  
```
2. Follow the setup instructions in the repository [README](https://github.com/onecx/onecx-ai-refactoring-agents/blob/main/angular/updates/README.md).

**Usage**

To migrate from Angular 18 to Angular 19, use the following command in your AI assistant:

```bash
/migrate-19
```

The migration agent will guide you through the pre-migration and post-migration steps, including PrimeNG updates if applicable.

## [](#migration-steps-before-angular-19)Migration Steps before upgrading to Angular 19

To simplify the migration process, it is recommended to complete the following steps before upgrading to Angular 19\. You can click the name of any change to open a detailed migration guide with instructions, code examples, and explanations.

* [Remove @onecx/keycloak-auth](remove-keycloak-auth.html)
* [Update Component Imports](update-component-imports.html)
* [Replace Removed Components](switch-to-new-components.html)
* [Adjust Packages in Webpack Config](adjust-packages-in-webpack-config.html)
* [Remove MenuService](remove-menuservice.html)
* [Update Translations](update-translations.html)

After these steps are completed, it is recommended to build the application to ensure that there are no remaining issues before proceeding with the Angular 19 upgrade:

```bash
npm run build
```

## [](#upgrade-to-angular-19)Upgrade to Angular 19

After completing the pre-migration steps, you can proceed with upgrading your application to Angular 19.

If the project is an NX workspace, follow the instructions in [Upgrade NX Application to Angular 19](upgrade-nx-angular-version.html). After completing the NX migration steps, also review the official Angular update guide for any additional steps or considerations: [Angular Update Guide](https://angular.dev/update-guide?v=18.0-19.0&l=3).

If the project is not an NX workspace, follow the official Angular update guide to perform the version upgrade by following this link: [Angular Update Guide](https://angular.dev/update-guide?v=18.0-19.0&l=3).

## [](#migration-steps-after-angular-19)Migration Steps after upgrading to Angular 19

Once the previous steps are completed, **the application should be upgraded to Angular 19 and libs v6 should be installed**. After the version updates are completed, the remaining steps of the migration can be followed:

* [Required Package Updates](update-packages.html)
* [Update FilterType Value](update-filtertype-value.html)
* [Update ConfigurationService Usage](update-configuration-service-usage.html)
* [Update Component Imports after Migration](update-component-import-post-migration.html)
* [Update Portal API Configuration object parameters](update-portal-api-configuration.html)
* [Remove @onecx/portal-layout-styles](remove-portal-layout-styles.html)
* [Remove addInitializeModuleGuard()](remove-add-initialize-module-guard.html)
* [Remove PortalCoreModule](remove-portal-core-module.html)
* [Adjust Standalone Mode](adjust-standalone-mode.html)
* [Replace BASE\_URL injection token](update-base-url.html)
* [Update Theme Service usage](update-theme-service.html)
* [Add Webpack Plugin for PrimeNG](add-required-plugin-to-primeng.html)
* [Add Webpack Plugin for Angular Material](add-angular-material-plugin.html)
* [Provide ThemeConfig](provide-theme-config.html)
* [Update Webpack Config to Use Dynamic Shared Entries](update-webpack-config.html)
