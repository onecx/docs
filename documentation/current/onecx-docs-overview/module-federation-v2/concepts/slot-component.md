# Slot Component

## [](#%5Foverview)Overview

The slot component mechanism in OneCX is used for dynamically rendering remote components in specific locations on a page using **Module Federation**. Slots are configurable at runtime.

Remote component loading is handled by the slot component. The remote component loading mechanism can be found [here](../../architecture/remote-components.html).

## [](#%5Fkey%5Faspects)Key aspects

* The loading process starts when a slot component is rendered on a page.
* Exposed remote component content is loaded using `@angular-architects/module-federation`.
* After successful loading, the component is rendered inside the slot component.
* Rendering uses a dynamic content creation mechanism based on the chosen expose method.

## [](#%5Fslot%5Frendering%5Fprocess)Slot rendering process

The following flow describes how slot rendering works:

* App1 owns the page and defines a **slot location**.
* App2 exposes a **remote component** using **module federation** that can be used in the slot.
* Both App1 and App2 are available in the **workspace**.
* The slot defined in App1 is **activated** in the **workspace**.
* A remote component from App2 is **assigned** to the slot in App1.
* When the slot is displayed, App1 dynamically loads the component **exposed** by App2 using **module federation**.
* The component is then **rendered** in the slot using the technology defined in the **remote component configuration**.

__Table 1\. Navigation__
| [← Previous: Shell UI Router](shell-router.html) | [Next: Expose Method →](expose-method.html) |
| ------------------------------------------------ | ------------------------------------------- |
