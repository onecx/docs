# Concepts

This section holds OneCX’s core platform concepts as short, public, technology-agnostic overviews, suitable for any OneCX developer. Each page introduces a concept and links out to the internal developer docs for the full deep dive.

## [](#concepts-pages)Pages

* [Routing](routing.html) — why a OneCX app’s routing must adapt to the shell’s base path, and how links between applications resolve.
* [Theming](theming.html) — how the shell and the OneCX Theme Management application provide the theme, expressed as CSS variables (design tokens) available on every page.
* [Translations](translations.html) — how OneCX applications provide multi-language support through per-language translation files.
* [Assets](assets.html) — what **assets** are in OneCX (icons, images, fonts, and i18n files) and why they need special treatment.
* [Authentication](authentication.html) — how the shell owns the entire authentication flow and session, and the small set of interactions an integrated app is limited to.
* [Style Isolation](style-isolation.html) — the rules OneCX places on application styles so they stay confined to the region each app renders into.
* [Module Federation](module-federation.html) — the mechanism that lets OneCX compose many independently developed and independently deployed applications at runtime.
* [Remote Components](remote-components.html) — how a piece of UI owned by one application can be embedded inside another, and the **Slots** that host them.
* [State Management](state-management.html) — how OneCX Angular applications use NgRx to model the data that drives their UI as a single, predictable store.
