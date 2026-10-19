# Local-only Testing

If a change is confined to a library, verify logic with the library’s unit tests and UI surfaces with Storybook. Library-local verification therefore uses unit tests for logic and Storybook for UI; no shell, no application, and no local OneCX environment are required when those suffice. Verify in the **onecx-portal-ui-libs** repository alone.

If the library change later needs shell or application verification, continue with Integration testing. If the source change is confined to a single OneCX application, use Application-only testing instead.

## [](#running-the-tests)Running the tests

1. Run the unit tests. The repository root exposes an `nx` test target that runs the tests of the affected projects:  
```bash  
npm test  
```
2. If the change affects how a component looks or behaves, also open the Storybook for the affected library to inspect it manually. Every Angular library exposes a `storybook` `nx` target:  
```bash  
nx run <library>:storybook  
```  
For example, to open the Storybook of `angular-accelerator`:  
```bash  
nx run angular-accelerator:storybook  
```

## [](#next)When the change needs more than the library’s own tests

If the source change is a library and it has to run inside the OneCX Shell and one or more local applications, continue with the [Integration testing](integration.html) guide. If the source change is confined to a single OneCX application, use the [Application-only testing](application-only.html) guide.

## [](#related)Related

* [Contribution & Testing](index.html) — the overview and the other verification tiers.
* [Integration testing](integration.html) — building the libraries locally and copying them into the shell and apps.
* [Application-only testing](application-only.html) — testing a change confined to a single application.
