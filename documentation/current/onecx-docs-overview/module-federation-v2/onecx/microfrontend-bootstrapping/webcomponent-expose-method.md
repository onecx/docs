# undefined

### [](#content-exposed-using-webcomponent-method)Content Exposed Using Webcomponent Method

[Loading mechanism for modules and Remote Components exposed using Webcomponent method](../angular-webcomponents.html#onecx-angular-webcomponents) requires that content is adapted to using Web Components Custom Elements. For both content types, bootstrapping logic needs to register a Custom Element in the Custom Elements Registry.

| |  For Angular-based content, apart from Custom Element registration, it is also required to cover a few Angular-related issues. For more information on those issues, please refer [here](../../concepts/webcomponents/expose-content-as-webcomponent.html#angular%5Fissues). |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

It is recommended to use the [@onecx/angular-webcomponents](../angular-webcomponents.html#onecx-angular-webcomponents) library to bootstrap Microfrontend’s content using its exposed methods. This library will be used in the examples throughout this document.

__Table 1\. Navigation__
| [← Previous: Content Exposed Using Angular Method](angular-expose-method.html) | [Next: Back to Microfrontend Bootstrapping →](index.html) |
| ------------------------------------------------------------------------------ | --------------------------------------------------------- |
