# NgRx

NgRx is a reactive state management library for Angular based on the Redux pattern and powered by RxJS. It helps you model application state as a single immutable source of truth, describe state changes with actions, and derive view data with selectors and effects.

| |  NgRx applies to Angular applications only. There is currently no equivalent state-management pattern documented for React applications in OneCX. |
| --------------------------------------------------------------------------------------------------------------------------------------------------- |

For why OneCX Angular applications use NgRx, see the [State Management](../concepts/state-management.html) concept page.

## [](#ngrx-what-is-ngrx)What Is NgRx?

* A set of libraries for Angular to manage global and feature state in a predictable and testable way.
* Core building blocks:  
   * Actions: Plain events that describe what happened.  
   * Reducers: Pure functions that compute new state from the previous state and an action.  
   * Selectors: Memoized queries to read and derive data from state.  
   * Effects: Side-effect handlers for async work (HTTP, routing, etc.).  
   * Entity/ComponentStore/Router Store/DevTools: Optional libraries to simplify common patterns.

## [](#ngrx-overview)Overview

Use NgRx when you need any of the following:

* Shared state across multiple routes/components and modules.
* Complex async orchestration (load, cache, error handling, retries).
* Auditability and predictability (time-travel debugging, action logs).
* Derived data that benefits from memoization via selectors.

Prefer local component state or `ComponentStore` for purely local/ephemeral UI concerns. Avoid putting computed/derivable data into the store; compute it via selectors instead.

## [](#ngrx-core-packages)Core Packages

* Store: `@ngrx/store` — application and feature state containers.
* Effects: `@ngrx/effects` — side-effects and async flows.
* Entity: `@ngrx/entity` — helpers for collections (ids, dictionaries, adapters).
* Router Store: `@ngrx/router-store` — integrates Angular Router state.
* ComponentStore: `@ngrx/component-store` — local, component-scoped state management.
* Store DevTools: `@ngrx/store-devtools` — time-travel debugging via Redux DevTools.

## [](#ngrx-pages)Pages in this section

* [Setup](ngrx/setup.html) — installing NgRx and the OneCX libraries, getting-started steps, and wiring OneCX platform state into the store.
* [Guidelines](ngrx/guidelines.html) — the OneCX NgRx conventions, project structure, dialogs, and the OneCX utility libraries.
* [Lazy Loading Tabs](ngrx/lazy-loading.html) — loading tabs dynamically with NgRx.
* [Search Criteria](ngrx/search-criteria/search-criteria.html) — adding search criteria to a search page:  
   * [AutoComplete](ngrx/search-criteria/autocomplete/autocomplete.html)  
   * [Calendar](ngrx/search-criteria/calendar.html)  
   * [Dropdown](ngrx/search-criteria/dropdown.html)  
   * [MultiSelect](ngrx/search-criteria/multiselect.html)

## [](#ngrx-useful-links)Useful Links

* Official website: [NgRx](https://ngrx.io/)
* Documentation: [Docs](https://ngrx.io/docs)
* Store: [Store](https://ngrx.io/guide/store)
* Effects: [Effects](https://ngrx.io/guide/effects)
* Entity: [Entity](https://ngrx.io/guide/entity)
* ComponentStore: [ComponentStore](https://ngrx.io/guide/component-store)
* Router Store: [Router Store](https://ngrx.io/guide/router-store)
* DevTools: [Store DevTools](https://ngrx.io/guide/store-devtools)
* Schematics: [Schematics](https://ngrx.io/guide/schematics)
