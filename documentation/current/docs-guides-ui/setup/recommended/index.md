# Recommended Setup

Recommended Setup covers the steps an application **should** complete to behave correctly in the OneCX shell. Unlike Required Setup, skipping any of these steps does not break the app outright — it still loads and runs — but it behaves **visibly incorrectly**: wrong or missing styles, missing or broken translations, or broken navigation.

This tier applies to both paths of building a OneCX UI:

* **Migrating an existing app** — bring a vanilla Angular or React application up to this checklist after completing [Required Setup](../required/index.html). See [Migrate Angular App to OneCX](../../angular/app-to-onecx.html) for the migration path itself; it cross-links back into these pages rather than restating their steps.
* **Creating a new app from scratch** — use this checklist, alongside Required Setup, as the target end-state for a freshly generated application.

| |  If a step isn’t listed here, it belongs to a different tier. Steps every app **must** complete to function at all belong to [Required Setup](../required/index.html). An Optional tier (steps an app **may** adopt with no correctness impact if skipped) is planned alongside this Recommended tier as part of the same three-tier Setup structure. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#recommended-setup-pages)Pages

* [Expose Component Styles](expose-component-styles.html) — how to expose an application’s and its libraries' `styles.css` in the build output, so the shell can style the app.
* [Apply Theming](apply-theming.html) — introduces OneCX theme variables and why application styles should use them; links to [Theming](#documentation:docs-guides-ui:concepts/theming.adoc) for the full deep dive.
* [Expose Library Assets](expose-library-assets.html) — how to expose the static assets (e.g. icons) of the OneCX libraries an application depends on, since Micro Frontends are loaded relative to the shell.
* [Adapt Routing](adapt-routing.html) — introduces why routing needs adaptation since Micro Frontends are relative to the shell; links to [Routing](#documentation:docs-guides-ui:concepts/routing.adoc) for the full deep dive.
