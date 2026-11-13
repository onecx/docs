# Release Overview

This page gives a high-level view of what is coming for the OneCX UI libraries and OneCX Shell. It is a planning overview, not a step-by-step guide. For the details of a specific upgrade, follow the links into the migration guides.

## [](#release-mapping)Release mapping

This table describes the current release plan. It is a planning baseline and may change.

| **Release** | **Shell (highest supported Angular version)** | **Core apps** | **Quarkus**      |
| ----------- | --------------------------------------------- | ------------- | ---------------- |
| Feb-27      | Angular 22                                    | Angular 19    | 3.40 LTS         |
| May-27      | Angular 22                                    | Angular 20    | 3.40 LTS         |
| Aug-27      | Angular 22                                    | Angular 21    | April-27 LTS     |
| Nov-27      | Angular 23                                    | Angular 22    | April-27 LTS     |
| Feb-28      | Angular 23                                    | Angular 23    | September-27 LTS |

## [](#onecx-libs)OneCX UI Libraries

The OneCX UI libraries are moving to a fully open-source stack in two stages. The two stages target different Angular versions and are delivered separately.

### [](#libs-release-timeline)Release timeline

Status is Released or Planned. For a planned item, the date is the current ETA.

| **Item**                                     | **Status** | **Date** |
| -------------------------------------------- | ---------- | -------- |
| Angular 22 (Optimus UI)                      | Planned    | 11.2026  |
| Angular 23 (Angular Material + Tailwind CSS) | Planned    | 2027     |

### [](#onecx-libs-angular-22)Angular 22, Optimus UI

The `@onecx/*` UI libraries move from **PrimeNG** to **Optimus UI** in **version 9.0.0**. Optimus UI is an open-source fork of PrimeNG that keeps its API. OneCX keeps its own libraries open source, and applications stay close to the PrimeNG APIs they already use.

Key points:

* Optimus UI replaces PrimeNG.
* PrimeNG-style component APIs are preserved.
* A few public entry points are renamed.
* Bump to libraries v9.0.0 and the Angular 22 toolchain.
* The Shell adds an Angular 22 preloader.

For the full, step-by-step guide to migrating an application to Angular 22 with the Optimus UI change, see the [Angular 22 migration guide](../onecx-portal-ui-libs/migrations/angular-22/migration-plan.html).

### [](#onecx-libs-angular-23)Angular 23, Angular Material + Tailwind CSS

OneCX rebuilds the `@onecx/*` accelerator components on **Angular Material** and **Tailwind CSS** with **Angular 23** support. Tailwind CSS is maintained by the Angular team.

Key points:

* Optimus UI support is retained.
* Accelerator components move to Angular Material.
* Public component APIs stay stable.
* A larger, multi-stage effort than Angular 22.
* Spans roughly two release cycles.

The Angular 23 migration guide and its step-by-step sections are being published as the work is finalized.

## [](#shell-upgrades)Shell Upgrades

The current planned Shell versions are listed in the [release mapping](#release-mapping).

### [](#shell-release-timeline)Release timeline

See the [release mapping](#release-mapping) for the current plan; planned releases may change.

The Shell’s current release notes are available in the [OneCX Shell documentation](../onecx-shell/v3/v3-release.html).

## [](#core-apps-upgrades)Core Apps Upgrades

The current planned Core Apps versions are listed in the [release mapping](#release-mapping).

### [](#core-apps-release-timeline)Release timeline

See the [release mapping](#release-mapping) for the current plan; planned releases may change.
