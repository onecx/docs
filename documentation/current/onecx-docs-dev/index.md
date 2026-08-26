# OneCX Development Documentation

This page brings together the collective knowledge of the Onecx community around best practices for creating Onecx software products.  
Here a selection of important resources to get you started:

* [Documentation](../onecx-docs-doc/index.html)
* [Local Environment](../onecx-local-env/index.html)
* [Quarkus](quarkus.html)
* [UI App Generator](../onecx-nx-plugins/index.html)
* [UI Troubleshooting](../docs-guides-ui/troubleshooting.html)

## [](#purpose-value)Purpose & Value

* Orientation: quick overview of areas, concepts, and timelines.
* Context: positioning of products, UIs, services, and architectures.
* Paths: targeted entry points for different roles (engineering, operations, product).

## [](#topic-map)Topic Map

* Platform Overview: vision, product landscape, core components.
* Architecture & Components: Shell, BFFs, services, data, Traefik.
* Domain Concepts: tenancy, permissions, profile, theme, workspace.
* Development Workflows: local setup, generator, CI/CD fundamentals.
* UI Libraries & Patterns: design system, reuse, best practices.
* Security & Tenancy: OIDC, Keycloak, tenant context, permissions.
* Data & Integrations: Postgres, REST APIs, configurations.
* Operations & Tooling: logs, health checks, Traefik dashboard, profiles.

## [](#entry-paths)Entry Paths

* Beginner: foundational concepts and first working setup.
* Builder: app creation (manual/CLI), hot reload, multiple apps.
* Integrator: interplay of UIs and services, routing, profiles.

## [](#quick-start-links)Quick Start Links

* Getting Started: see ./index.adoc\[OneCX Getting Started\]
* First Application (overview): ./first-app/create\_angular\_app.adoc\[First Angular App\]
* Manual setup: ./first-app/app\_setup\_manual.adoc\[Manual App Setup\]
* CLI setup: ./first-app/app\_setup\_cli.adoc\[App Setup via CLI\]
* Hot reload: ./first-app/enable\_hot\_reload.adoc\[Enable Hot Reload\]
* Multiple apps: ./first-app/run\_multiple\_apps.adoc\[Run Multiple Apps\]
* Image build (manual): ./first-app/image\_build\_manual.adoc\[Manual Image Build\]
* Image build (automatic): ./first-app/image\_build\_automatic.adoc\[Automatic Image Build\]
* Test core apps: ./first-app/testing\_existing\_core\_apps.adoc\[Testing Existing Core Apps\]

## [](#practical-tips)Practical Tips

* Traefik uses path prefixes like `/mfe/<app>/`; align your dev server base href accordingly.
* Use Docker Compose profiles to start only the services you need.
* The Traefik dashboard helps analyze routing and health checks.

## [](#conventions)Conventions

* Consistent paths, naming conventions, and shared UI patterns ease integration.
* Prefer reusable libraries from `onecx-portal-ui-libs`.

## [](#contribute)Contribute

* Contributions welcome: add content, report gaps, improve examples.
* Follow the existing structure and link appropriately.
