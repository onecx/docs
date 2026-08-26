# Optional debugging preference: debug-js namespaces

In v8, OneCX libraries `console.log` usage was removed in favor of namespace-based debug logging.OneCX libraries use [debug](https://www.npmjs.com/package/debug) (aka **debug-js**) for runtime logging.

This is not a breaking change for consumers.

## [](#%5Fenable%5Flogging)Enable Logging

Use this only as a debugging preference when troubleshooting.

For troubleshooting, enable logs via browser local storage:

```js
localStorage.debug = '@onecx*'
location.reload()
```

You can narrow logging to specific libraries, for example:

```js
localStorage.debug = '@onecx/angular-auth*'
location.reload()
```

See also [Browser Logging](../../browser-logging.html) for more details on how to use debug-js namespaces for troubleshooting and debugging purposes.
