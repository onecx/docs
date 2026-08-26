# NgRx

## [](#what-is-ngrx)What Is NgRx?

* A set of libraries for Angular to manage global and feature state in a predictable and testable way.
* Core building blocks:  
   * Actions: Plain events that describe what happened.  
   * Reducers: Pure functions that compute new state from the previous state and an action.  
   * Selectors: Memoized queries to read and derive data from state.  
   * Effects: Side-effect handlers for async work (HTTP, routing, etc.).  
   * Entity/ComponentStore/Router Store/DevTools: Optional libraries to simplify common patterns.

## [](#overview)Overview

Use NgRx when you need any of the following: \* Shared state across multiple routes/components and modules. \* Complex async orchestration (load, cache, error handling, retries). \* Auditability and predictability (time-travel debugging, action logs). \* Derived data that benefits from memoization via selectors.

Prefer local component state or `ComponentStore` for purely local/ephemeral UI concerns. Avoid putting computed/derivable data into the store; compute it via selectors instead.

## [](#core-packages)Core Packages

* Store: `@ngrx/store` — application and feature state containers.
* Effects: `@ngrx/effects` — side-effects and async flows.
* Entity: `@ngrx/entity` — helpers for collections (ids, dictionaries, adapters).
* Router Store: `@ngrx/router-store` — integrates Angular Router state.
* ComponentStore: `@ngrx/component-store` — local, component-scoped state management.
* Store DevTools: `@ngrx/store-devtools` — time-travel debugging via Redux DevTools.

## [](#getting-started)Getting Started

Install commonly used packages:

```bash
npm install @ngrx/store @ngrx/effects @ngrx/entity @ngrx/router-store @ngrx/store-devtools
```

High-level steps: 1\. Define actions for user intents and async outcomes. 2\. Create feature state, initial state, and reducers. 3\. Add selectors to expose view models from state. 4\. Implement effects to handle HTTP calls, routing, and other side effects. 5\. Wire up the feature with `provideState`/`provideEffects` (standalone) or feature modules. 6\. Use the Redux DevTools for debugging (`StoreDevtoolsModule` or `provideStoreDevtools`).

## [](#onecx-guides-and-examples)OneCX Guides and Examples

* [Lazy Loading Tabs with NgRx](lazy-loading.html)
* Adding Search Criteria:  
   * [Search Criteria](search-criteria/search-criteria.html)  
   * [Autocomplete](search-criteria/autocomplete/autocomplete.html)  
   * [Calendar](search-criteria/calendar.html)  
   * [Dropdown](search-criteria/dropdown.html)  
   * [MultiSelect](search-criteria/multiselect.html)

## [](#useful-links)Useful Links

* Official website: [NgRx](https://ngrx.io/)
* Documentation: [Docs](https://ngrx.io/docs)
* Store: [Store](https://ngrx.io/guide/store)
* Effects: [Effects](https://ngrx.io/guide/effects)
* Entity: [Entity](https://ngrx.io/guide/entity)
* ComponentStore: [ComponentStore](https://ngrx.io/guide/component-store)
* Router Store: [Router Store](https://ngrx.io/guide/router-store)
* DevTools: [Store DevTools](https://ngrx.io/guide/store-devtools)
* Schematics: [Schematics](https://ngrx.io/guide/schematics)
