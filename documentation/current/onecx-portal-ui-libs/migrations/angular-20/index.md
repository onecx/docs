# Migrate OneCX App from Angular 19 to Angular 20

## [](#overview)Overview

This guide provides comprehensive step-by-step instructions for migrating OneCX applications from Angular 19 to Angular 20\. As part of upgrading to Angular 20, you must update your OneCX UI libraries to version 7\. This library update is not a standalone migration but a required part of the Angular version upgrade process, as OneCX v7 libraries provide Angular 20 compatibility and include necessary breaking changes.

## [](#prerequisites)Prerequisites

Before starting this migration:

* Your OneCX application is currently running on Angular 19
* You have OneCX UI libraries v6.x installed
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
/migrate-20
```

The migration agent will guide you through the pre-migration and post-migration steps, including PrimeNG updates if applicable.

## [](#migration-steps-before-angular-20)Migration Steps before upgrading to Angular 20

To simplify the migration process, it is recommended to complete the following steps before upgrading to Angular 20\. You can click the name of any change to open a detailed migration guide with instructions, code examples, and explanations.

* [Remove keycloak-js from your application](remove-keycloak-js.html)
* [Remove @onecx/shell-core](remove-shell-core.html)

After these steps are completed, it is recommended to build the application to ensure that there are no remaining issues before proceeding with the Angular 20 upgrade:

```bash
npm run build
```

## [](#upgrade-to-angular-20)Upgrade to Angular 20

After completing the pre-migration steps, you can proceed with upgrading your application to Angular 20.

If the project is an NX workspace, follow the instructions in [Upgrade NX Application to Angular 20](update-nx-angular-version-20.html). After completing the NX migration steps, also review the official Angular update guide for any additional steps or considerations: [Angular Update Guide](https://angular.dev/update-guide?v=19.0-20.0&l=3).

If the project is not an NX workspace, follow the official Angular update guide to perform the version upgrade by following this link: [Angular Update Guide](https://angular.dev/update-guide?v=19.0-20.0&l=3).

## [](#migration-steps-after-angular-20)Migration Steps after upgrading to Angular 20

Once the previous steps are completed, **the application should be upgraded to Angular 20 and libs v7 should be installed**. After the version updates are completed, the remaining steps of the migration can be followed.

* [Required Package Updates](update-v7-packages.html)
* [Adjust ngrx-accelerator library utilities](adjust-ngrx-accelerator.html)
* [Update package imports for PrimeNG theming](update-primeng-package.html)
* [Update package imports for style utilities](update-style-package.html)
* [Migrate to OnecxTranslateLoader translation mechanism](migrate-to-onecx-translate-loader.html)
* [Use updated ObjectDetailItem interface for PageHeaderComponent](use-new-object-detail-item-interface.html)
* [Be aware of the PortalDialogService signature changes](portal-dialog-service-signature-changes.html)
* [Leverage Angular guards](updated-guards-usage.html)
