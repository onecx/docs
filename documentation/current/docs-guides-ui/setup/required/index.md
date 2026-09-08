# Required Setup

Required Setup covers the steps every application **must** complete to function in the OneCX shell at all. Skipping any of them results in a broken integration (the app fails to load, cannot route, or cannot authenticate), not merely a degraded one.

This tier applies to both paths of building a OneCX UI:

* **Migrating an existing app** — bring a vanilla Angular or React application up to this checklist. See [Migrate Angular App to OneCX](../../angular/app-to-onecx.html) for the migration path itself; it cross-links back into these pages rather than restating their steps.
* **Creating a new app from scratch** — use this checklist as the target end-state for a freshly generated application.

| |  If a step isn’t listed here, it belongs to a different tier. See [Recommended Setup](../recommended/index.html) for steps an app **should** complete to behave correctly, not just to run. An Optional tier (steps an app **may** adopt with no correctness impact if skipped) is planned alongside this Required tier as part of the same three-tier Setup structure. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#required-setup-pages)Pages

* [Platform & Package Compatibility Requirements](platform-package-compatibility.html) — the Angular version, package-version, and package-sharing constraints an app must satisfy to be compatible with the shell.
* [Expose a Remote Module](expose-remote-module.html) — how to expose an application’s module or component via Module Federation so the shell can load it.  
   * [Module Approach](expose-remote-module/module-approach.html)  
   * [Component Approach](expose-remote-module/component-approach.html)
* [Configure Remote Package Sharing](configure-remote-package-sharing.html) — how to assign the app and its shared dependencies to the correct Module Federation share scope.
* [Configure Authentication](configure-authentication.html) — how to ensure requests carry the shell’s authentication header.
