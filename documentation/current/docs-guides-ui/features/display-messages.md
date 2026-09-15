# Display Messages

In a OneCX deployment the application’s content is rendered inside the OneCX shell, which owns the page chrome. Instead of building and styling message UI of its own, an application can **display a message** and leave the rendering to the shell: the app triggers the message, the shell shows it. OneCX does not prescribe **when** or **how often** an application should display a message for a page event — the feature simply removes the need for every application to ship its own message UI.

## [](#display-messages-how-it-works)How it works

An application triggers a message by publishing it on the shared [MessageTopic](../../onecx-portal-ui-libs/libraries/integration-interface.html#message-topic). Each message carries:

* a **severity** — `success`, `info`, `warning`, or `error`; and
* an optional, **translated** summary and detail.

The summary and detail are not passed as literal text: the app supplies translation **keys** (and optional parameters), and the framework resolves them with the application’s translation setup before the message is published. This is the same mechanism the [Translations](../concepts/translations.html) concept uses for application content, so a message reads in the user’s current language.

The application does **not** own the display. After the message is published on the topic, the OneCX shell (or the standalone shell viewport, for standalone applications) subscribes to that topic and renders the message with a PrimeNG toast component. The message therefore appears through the shell’s UI and inherits the shell’s look and feel; the application only ever produces the message, it never builds or positions the toast.

## [](#display-messages-angular)Angular applications

Angular applications display messages through the `PortalMessageService` (from `@onecx/angular-integration-interface`). Inject the service and call one of the severity methods — `success()`, `info()`, `warning()`, or `error()` — passing a message object holding the translation keys and parameters. See the [PortalMessageService documentation](../../onecx-portal-ui-libs/service/portal-message-service.html) for usage and the full list of message properties.

## [](#display-messages-react)React applications

React applications display messages through the `PortalMessageProvider` and the `usePortalMessage` hook (from `@onecx/react-integration-interface`). Wrap the application (or the relevant subtree) in `PortalMessageProvider`, then read the `success`, `info`, `warning`, and `error` helpers from the hook in any component. See the [Portal Message Provider](../react/libraries/react-integration-interface.html#portal-message-provider) documentation for the full provider and hook API.

## [](#display-messages-related)Related

* [PortalMessageService](../../onecx-portal-ui-libs/service/portal-message-service.html) — the Angular service that publishes messages, including the full message-property reference.
* [React Portal Message Provider](../react/libraries/react-integration-interface.html#portal-message-provider) — the React provider and `usePortalMessage` hook.
* [MessageTopic](../../onecx-portal-ui-libs/libraries/integration-interface.html#message-topic) — the shared topic the application publishes messages on.
* [Translations](../concepts/translations.html) — how the summary and detail translation keys are resolved.
