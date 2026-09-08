# Apply Theming

An application integrated with OneCX still loads and runs even if it doesn’t use OneCX theme variables, but it renders with a theme that doesn’t match the rest of the shell. In OneCX, each workspace can use a different theme for its pages, and the shell makes the active theme’s CSS variables available on every page automatically — the application should use those variables in its own styles instead of hard-coded values.

See [Theming](#documentation:docs-guides-ui:concepts/theming.adoc) for the full list of available theme variables and how to use them in Angular and React applications.
