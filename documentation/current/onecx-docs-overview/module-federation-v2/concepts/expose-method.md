# Expose Method in Microfrontend Loading

## [](#%5Foverview)Overview

The expose method is a factor considered by the respective loading mechanism (Shell UI Router or Slot Component) to ensure correct content loading.

## [](#%5Fusage%5Fin%5Floading%5Fmechanisms)Usage in loading mechanisms

| Loading type             | Impact                                                         |
| ------------------------ | -------------------------------------------------------------- |
| Module loading           | The loadChildren method and router configuration are affected. |
| Remote component loading | A different mechanism for dynamic content creation is chosen.  |

More details about the impact of the expose method can be found [here](webcomponents/index.html).

__Table 1\. Navigation__
| [← Previous: Introduction to Module Federation](../../index.html) |
| ----------------------------------------------------------------- |
