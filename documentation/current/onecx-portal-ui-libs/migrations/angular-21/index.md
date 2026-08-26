# Migrate OneCX App from Angular 20 to Angular 21

## [](#overview)Overview

| |  This guide is a work in progress. Angular 21 support and OneCX UI libraries v8 are not final yet. Angular 21 support will be provided with OneCX Shell v3. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------- |

This guide provides step-by-step instructions for migrating OneCX applications from Angular 20 to Angular 21\. As part of upgrading to Angular 21, you must update your OneCX UI libraries to version 8\. This library update is not a standalone migration but a required part of the Angular version upgrade process, as OneCX v8 libraries provide Angular 21 compatibility and include required breaking changes.

## [](#prerequisites)Prerequisites

Before starting this migration:

* Your OneCX application is currently running on Angular 20
* You have OneCX UI libraries v7.x installed
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
/migrate-21
```

The migration agent will guide you through the pre-migration and post-migration steps, including PrimeNG updates if applicable.

## [](#migration-steps-before-angular-21)Migration Steps before upgrading to Angular 21

To simplify the migration process, it is recommended to complete the following steps before upgrading to Angular 21\. You can click the name of any change to open a detailed migration guide with instructions, code examples, and explanations.

* [Replace deprecated topic publisher classes](replace-topic-publishers.html)
* [Adjust ngrx utilities usage](adjust-ngrx-utilities.html)
* [Note: Onecx V8 bundling Changes](esm-bundling.html)

## [](#upgrade-to-angular-21)Upgrade to Angular 21

After completing the pre-migration steps, you can proceed with upgrading your application to Angular 21.

If the project is an NX workspace, follow the instructions in [Upgrade NX Application to Angular 21](update-nx-angular-version-21.html). After completing the NX migration steps, also review the official Angular update guide for any additional steps or considerations: [Angular Update Guide](https://angular.dev/update-guide?v=20.0-21.0&l=1).

If the project is not an NX workspace, follow the official Angular update guide to perform the version upgrade by following this link: [Angular Update Guide](https://angular.dev/update-guide?v=20.0-21.0&l=1).

## [](#migration-steps-after-angular-21)Migration Steps after upgrading to Angular 21

Once the previous steps are completed, **the application should be upgraded to Angular 21 and libs v8 should be installed**. After the version updates are completed, the remaining steps of the migration can be followed.

* [Required Package Updates](update-v8-packages.html)
* [Set shareScope values in Helm](add-share-scope-angular-21.html)
* [Move auth implementation imports from @onecx/angular-auth to @onecx/shell-auth](move-auth-to-shell-auth.html)
* [Update imports to supported public APIs](update-public-api-imports.html)
* [Optional: Setup Logging with debug-js namespaces](use-debug-logger-namespaces.html)
* [Update Webpack Config](../../../onecx-docs-dev/shell-integration/shell-v3-migration.html)
