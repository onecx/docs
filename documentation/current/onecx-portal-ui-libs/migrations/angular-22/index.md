# Migrate OneCX App from Angular 21 to Angular 22

## [](#overview)Overview

| |  This guide is a work in progress. Angular 22 support and OneCX UI libraries v9 are not final yet. Angular 22 support is provided with OneCX Shell v3. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- |

This guide provides step-by-step instructions for migrating OneCX applications from Angular 21 to Angular 22\. As part of upgrading to Angular 22, you must update your OneCX UI libraries to version 9\. This library update is not a standalone migration but a required part of the Angular version upgrade process, as OneCX v9 libraries provide Angular 22 compatibility and include required breaking changes.

OneCX UI libraries v9 change the component library the `@onecx/*` libraries are built on: from **PrimeNG** to **Optimus UI**, an open-source, community-maintained fork of PrimeNG that preserves the PrimeNG API. The reason for the move is that PrimeNG is no longer open source and is not compatible with the Angular 22 build; moving to Optimus UI keeps the OneCX libraries fully open source while letting consuming apps change little — the same PrimeNG-style selectors, inputs, and providers keep working. PrimeFlex is replaced by **Tailwind CSS v4** at the same time.

| |  This is the Angular 22 / v9 migration. A separate, later effort moves OneCX’s own components to Angular Material + Tailwind CSS. |
| ----------------------------------------------------------------------------------------------------------------------------------- |

## [](#prerequisites)Prerequisites

Before starting this migration:

* The OneCX application is currently running on Angular 21
* The OneCX UI libraries v8.x are installed
* The application builds and the tests are green before the migration starts
* A working development environment is available

## [](#ai-driven-migration-assistance)AI Driven Migration Assistance

To simplify the migration process, you can use the AI-driven migration assistant. The [OneCX AI Refactoring Agents](https://github.com/onecx/onecx-ai-refactoring-agents) repository provides a dedicated migration agent to automate the OneCX Angular migration process. Below is the migration agent setup, which you can copy and use with your preferred AI tool. These agents have been tested with GitHub Copilot (Claude Sonnet 4.6) in agent mode.

AI Migration Agent 

**Before You Start**

Make sure you have the Recommended MCP servers configured before running the migration agent. For detailed setup instructions, see the [MCP Server Setup Guide](../../../onecx-docs-dev/ai/mcp%5Fserver%5Fsetup.html) ([published reference](https://onecx.github.io/docs/documentation/current/onecx-docs-dev/ai/mcp%5Fserver%5Fsetup.html)).

**Setup**

1. Clone or pull the latest version of the repository:  
```bash  
git clone https://github.com/onecx/onecx-ai-refactoring-agents.git  
# or if already cloned:  
cd onecx-ai-refactoring-agents && git pull  
```
2. Follow the setup instructions in the repository [README](https://github.com/onecx/onecx-ai-refactoring-agents/blob/main/angular/updates/README.md).

**Usage**

To migrate from Angular 21 to Angular 22, use the following command in your AI assistant:

```bash
/migrate-22
```

The migration agent will guide you through the pre-migration and post-migration steps.

## [](#migration-steps-before-angular-22)Migration Steps before upgrading to Angular 22

To keep the migration verifiable on a single framework version at a time, complete the following steps before upgrading to Angular 22\. The name of any change opens a detailed migration guide with instructions, code examples, and explanations.

* [Update Node.js to a version supported by Angular 22](update-node-version.html)
* [Import shared library configuration helpers from @onecx/build-utils](use-build-utils-for-shared-config.html)
* [Migrate the application’s own PrimeNG usage to Optimus UI v1](migrate-to-optimus-ui-v1.html)

## [](#upgrade-to-angular-22)Upgrade to Angular 22

After completing the pre-migration steps, proceed with upgrading the application to Angular 22.

If the project is an NX workspace, follow the instructions in [Upgrade NX Application to Angular 22](update-nx-angular-version-22.html). After completing the NX migration steps, also review the official Angular update guide for any additional steps or considerations: [Angular Update Guide](https://angular.dev/update-guide?v=21.0-22.0).

If the project is not an NX workspace, follow the official Angular update guide to perform the version upgrade by following this link: [Angular Update Guide](https://angular.dev/update-guide?v=21.0-22.0).

* [Upgrade the toolchain to Angular 22](update-nx-angular-version-22.html)
* [Keep build-angular at 22.2.3 and webpack at 5.111.0](keep-build-angular-22-2-3-and-webpack.html)
* [Update the OneCX UI libraries to v9](update-onecx-libs-v9.html)

## [](#migration-steps-after-angular-22)Migration Steps after upgrading to Angular 22

Once the previous steps are completed, **the application should be upgraded to Angular 22 and the OneCX UI libraries v9 should be installed**. After the version updates are completed, the remaining steps of the migration can be followed.

* [PrimeFlex to Tailwind CSS v4](primeflex-to-tailwind-v4.html)
* [Set shareScope values in Helm](add-share-scope-angular-22.html)
