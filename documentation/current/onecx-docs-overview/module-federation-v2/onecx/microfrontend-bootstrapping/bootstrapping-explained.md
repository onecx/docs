# undefined

## [](#microfrontend-content-bootstrapping-explained)Microfrontend Content Bootstrapping Explained

[Microfrontend content loading](../../concepts/content-loading.html) is an action triggered by the route change (Shell Application’s responsibility of loading modules) or by the Slot Component display (Slot Component’s responsibility of loading Remote Components). During this action, Microfrontend’s content, exposed via remote entry file, is loaded and bootstrapped using the provided file in [Webpack configuration](../microfrontend-configuration.html).

Depending on the content type and chosen expose method, different adjustments have to be made to ensure correct content bootstrapping.

* [Content Exposed Using Angular Method](angular-expose-method.html)
* [Content Exposed Using Webcomponent Method](webcomponent-expose-method.html)

__Table 1\. Navigation__
| [← Previous: Microfrontend Bootstrapping](index.html) | [Next: Content Exposed Using Angular Method →](angular-expose-method.html) |
| ----------------------------------------------------- | -------------------------------------------------------------------------- |
