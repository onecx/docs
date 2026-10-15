# Features

This section holds standalone pages describing platform features an application may choose to adopt. Unlike the Setup tiers, adopting a feature has no correctness impact if skipped — the application still loads, runs, and behaves correctly without it. Each page is independent of the others.

## [](#features-pages)Pages

* [Multi-language](multi-language.html) — how an Angular application opts into fallback languages so a missing translation key resolves to a supported language instead of showing the raw key.
* [Display Messages](display-messages.html) — how an application triggers a message and leaves its rendering to the shell, instead of shipping its own message UI.
* [Permissions Handling](permissions.html) — how an application reacts to the permissions the platform assigns a user by rendering UI conditionally.
* [PrimeNG Theming Customization](primeng/theming-customization.html) — how to override PrimeNG design tokens at the application level so one application styles PrimeNG differently from every other application on the page.
* [Source Maps](development/source-maps.html) — how to enable source maps so browser developer tools can show the original source instead of the compiled build output.
* [Environment Variables](environment-variables.html) — how an application reads runtime configuration values (endpoints, auth settings, feature flags) that can change after the build.
* NgRx State Management — a practical guide to adopting the `@onecx/ngrx-*` libraries in an Angular application, pairing with [State Management](../concepts/state-management.html). This page is being authored and will be linked once it is published.
