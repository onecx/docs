# Browser Logging (debug-js)

OneCX UI libraries use [debug](https://www.npmjs.com/package/debug) (aka **debug-js**) for runtime logging.

This means:

* Logging is **disabled by default**.
* You enable logging in the browser by setting a value for `localStorage.debug` (or via a helper in DevTools).
* Log output is written to the browser console when enabled.

## [](#%5Fenable%5Flogging)Enable logging

You can enable logging by setting `localStorage.debug` and reloading the page.

```js
// Enable all OneCX UI library logs
localStorage.debug = '@onecx*'
location.reload()
```

## [](#%5Fcommon%5Fpatterns)Common patterns

`debug` uses namespace patterns. The following wildcards are commonly used:

* `*` matches anything
* comma-separated patterns are allowed
* prefixing a pattern with `-` excludes it

See the upstream documentation for the full syntax:

* [debug-js: Browser support](https://github.com/debug-js/debug#browser-support)

## [](#%5Fexamples)Examples

### [](#%5Fenable%5Feverything%5Fexcept%5Ftopic%5Fand%5Fgatherer)Enable everything except Topic and Gatherer

This is useful when you want general diagnostics but do not want event/data stream logs.

```js
// Enable all OneCX logs, but exclude Topic and Gatherer namespaces
localStorage.debug = '@onecx*,-@onecx*:Topic:*,-@onecx*:Gatherer:*'
location.reload()
```

### [](#%5Fenable%5Fonly%5Fa%5Fsingle%5Flibrary)Enable only a single library

```js
// Only angular-utils
localStorage.debug = '@onecx/angular-utils*'
location.reload()
```

### [](#%5Fenable%5Fa%5Flibrary%5Fa%5Fconcrete%5Flocation)Enable a library + a concrete location

```js
// Example: focus on a single component/service
localStorage.debug = '@onecx/angular-auth:AuthProxyService'
location.reload()
```

## [](#%5Fvalid%5Fonecx%5Fnamespaces)Valid OneCX namespaces

Namespaces are composed as:

```text
@onecx/<libOrAppName>:<location>:<level>
```

Where `<libOrAppName>` is the value passed to `createLoggerFactory(…​)`.

Where `<level>` is one of:

* `debug`
* `info`
* `warn`
* `error`

## [](#%5Floglevels%5Fwhen%5Fto%5Fuse%5Fwhat)Loglevels (when to use what)

The `debug` namespace includes the loglevel as the last segment. This allows you to filter by severity in the browser.

* `debug`: High-volume diagnostics for local development and deep troubleshooting (state transitions, inputs/outputs, timing).
* `info`: Important lifecycle milestones that are useful in normal troubleshooting (initialization, successful operations, configuration decisions).
* `warn`: Unexpected situations that the app can recover from (fallback paths, invalid user input that is handled, missing optional dependencies).
* `error`: Failures that prevent a feature from working or indicate a bug (exceptions, failed network calls that break functionality, invalid critical configuration).

As a rule of thumb:

* Prefer `debug` for details you don’t want enabled in normal troubleshooting.
* Prefer `info` for "what happened" breadcrumbs.
* Use `warn` when something is off but you can still proceed.
* Use `error` when you cannot proceed or you need attention.

## [](#%5Fexamples%5Fby%5Floglevel)Examples by loglevel

```js
// Everything (all libraries, all locations, all levels)
localStorage.debug = '@onecx*'
location.reload()

// Only errors across all OneCX libraries
localStorage.debug = '@onecx*:*:error'
location.reload()

// Only warnings + errors (by combining patterns)
localStorage.debug = '@onecx*:*:warn,@onecx*:*:error'
location.reload()

// Only debug logs for a single location
localStorage.debug = '@onecx/angular-auth:AuthProxyService:debug'
location.reload()
```

### [](#%5Flibrary%5Fnamespaces)Library namespaces

These namespaces exist in the current repo:

* `@onecx/accelerator`
* `@onecx/angular-accelerator`
* `@onecx/angular-accelerator:testing`
* `@onecx/angular-auth`
* `@onecx/angular-integration-interface`
* `@onecx/angular-integration-interface:mocks`
* `@onecx/angular-remote-components`
* `@onecx/angular-remote-components:mocks`
* `@onecx/angular-remote-components:testing`
* `@onecx/angular-standalone-shell`
* `@onecx/angular-testing`
* `@onecx/angular-utils`
* `@onecx/angular-utils:guards`
* `@onecx/angular-utils:mocks`
* `@onecx/angular-utils:style`
* `@onecx/angular-utils:theme/primeng`
* `@onecx/angular-webcomponents`
* `@onecx/integration-interface`
* `@onecx/ngrx-accelerator`
* `@onecx/ngrx-integration-interface`

### [](#%5Fspecial%5Fruntime%5Fnamespaces)Special runtime namespaces

Some logs are intentionally high-volume and are separated into dedicated namespaces:

* `@onecx/accelerator:Topic:<name>` and `@onecx/accelerator:TopicPublisher:<name>`
* `@onecx/accelerator:Gatherer:<name>`

These are excluded in the example above.
