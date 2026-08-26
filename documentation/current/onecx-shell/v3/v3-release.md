# Shell V3

## [](#summary)Summary

OneCX Shell UI 3.0.0 is a major platform release that introduces a new integration path for Angular 21 while continuing to support previously supported Angular application versions. It also advances the shell layout model with updated slot-group conventions, improves startup and runtime efficiency, and delivers enhancements for shell integration, responsiveness, and deployment support.

Because this release includes platform-level and integration-related changes, it should be validated carefully in consumer environments, especially where custom slot configuration, microfrontend integration, or deployment-specific settings are in use.

## [](#upgrade-notes)Important Upgrade Notes

With the v3 release, all previously supported Angular application versions continue to be supported, and no immediate migration actions are required for Angular applications. No required configuration changes are needed.

It is recommended to validate shell integration, configuration, and deployment behavior in a non-production environment before promoting to production and consider the [Shell v3 Migration Guide](../../onecx-docs-dev/shell-integration/shell-v3-migration.html). It contains relevant information for ensuring a smooth upgrade process for applications and environments.

| |  This is a major release. Consumers should validate shell integration, configuration, and deployment behavior before promoting to production. |
| ----------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#highlights)Highlights

* Introduces a new Angular 21 integration path while maintaining compatibility for previously supported applications
* Enhances shell layout and extensibility with viewport restructuring and slot-group based layout conventions
* Improves startup and runtime efficiency, including reduced message exchange between microfrontends
* Adds new shell capabilities including an About page and source maps support

## [](#release-notes)Release Notes

### [](#angular-21-support)Angular 21 support with shareScope

Shell v3 introduces changes to microfrontend integration to support Angular 21 applications using a dedicated module federation share scope. This allows Angular 21 applications to integrate with the shell while maintaining compatibility with previously supported Angular versions. For details on required share scopes and migration actions, see [What share scopes are needed](../../docs-guides-ui/ui-additional/share-scopes.html).

### [](#layout-improvements)Shell layout and extensibility improvements

The shell layout model has been enhanced with viewport restructuring and new slot-group based layout conventions. This provides improved flexibility and extensibility for application integration and layout configuration. For details on the new layout model and migration actions, see [V3 Shell Layout](v3-shell-layout.html) and [Shell v3 Migration Guide](../../onecx-docs-dev/shell-integration/shell-v3-migration.html).

### [](#about-page)About page

Shell v3 introduces a new About page that provides information about the supported Angular versions. For more details, see [About Page](../../onecx-shell-ui/onecx-shell-ui-docs.html#primary-method-about-page).

### [](#source-maps-support)Source maps support

Shell v3 adds support for source maps, which can be enabled to facilitate debugging of integrated applications. For details on how to enable source maps, see [Enable Shell Source Maps](../enable-shell-source-maps.html).

### [](#efficiency-improvements)Efficiency improvements

Shell v3 includes various improvements to startup and runtime efficiency, including optimizations to reduce message exchange between microfrontends. These improvements can lead to faster load times and improved performance for integrated applications.

## [](#migration-checklist)Migration Checklist

To ensure a smooth migration to Shell v3, consider the following checklist:

* Review the [Shell v3 Migration Guide](../../onecx-docs-dev/shell-integration/shell-v3-migration.html) for detailed information on changes and migration actions.
* Validate shell integration with applications and configuration in a non-production environment before promoting to production.
* Validate application layout after migration, especially if using custom styling rules that may be affected by the new layout model.

## [](#references)References

* Release: <https://github.com/onecx/onecx-shell-ui/releases/tag/3.0.0>
* Full changelog: <https://github.com/onecx/onecx-shell-ui/compare/2.4.0…​3.0.0>
* Shell v3 migration guide: [Shell v3 Migration Guide](../../onecx-docs-dev/shell-integration/shell-v3-migration.html)
* OneCX UI libraries Angular 21 migration guide: <https://github.com/onecx/onecx-portal-ui-libs/blob/a2cbe83f338710f46d561e043c32c0dda6b1d2a4/docs/modules/onecx-portal-ui-libs/pages/migrations/angular-21/index.adoc>
