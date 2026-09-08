# Configure Authentication

Every application integrated with OneCX must ensure that all outgoing HTTP requests carry the shell’s authentication headers.

## [](#angular-applications)Angular Applications

Import `AngularAuthModule` from `@onecx/angular-auth` in the application’s bootstrap providers. It registers an HTTP interceptor that automatically attaches the required authentication headers to outgoing requests.

## [](#react-applications)React Applications

React applications must use an HTTP client setup that attaches the shell authentication headers to outgoing requests. For the OneCX React helper library, see [@onecx/react-auth](../../react/libraries/react-auth.html).

## [](#advanced-topics)Advanced Topics

For the shell-owns-auth model, sending a logout event, using the auth proxy directly, configuring a custom authentication service, and token refresh, see [Authentication](../../concepts/authentication.html).
