# Content Type in Microfrontend Loading

## [](#%5Foverview)Overview

Content Type defines what kind of UI is dynamically loaded as a microfrontend in the OneCX platform.

It determines whether you are loading a full feature (Module) or a reusable UI component (Remote Component).

Selecting the correct content type is important, as it affects how the microfrontend is loaded and displayed.

## [](#%5Fcontent%5Ftype%5Fselection)Content Type Selection

__Table 1\. Content Type Selection__
| Use Case                                 | Content Type     | Loading Mechanism                     |
| ---------------------------------------- | ---------------- | ------------------------------------- |
| Full page or feature with routing        | Module           | [Shell UI Router](shell-router.html)  |
| Reusable UI component embedded in a page | Remote Component | [Slot Component](slot-component.html) |

__Table 2\. Navigation__
| [← Previous: Microfrontend Content Loading](content-loading.html) | [Next: Shell UI Router →](shell-router.html) |
| ----------------------------------------------------------------- | -------------------------------------------- |
