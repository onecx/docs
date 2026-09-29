# Environment Variables

OneCX UI applications read **environment variables** as runtime configuration values: endpoints, auth settings, feature flags, and similar values that may differ between deployments. Unlike build-time constants, these values can change after the application has been built, so they are delivered to the running browser at startup.

This page explains where those values are read from, how to make sure they are present in a given deployment, and how to apply changes to the Shell and to an individual application.

| |  Runtime configuration is loaded into the browser and is therefore **public**. Never store secrets (passwords, private keys, client secrets, tokens) in runtime configuration. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#environment-variables-services)The services that read configuration

All OneCX UI configuration is read through the integration-interface package. Two services own the values, split by scope:

* **[AppConfigService](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#app-config-service)** — **application (MFE) scope**. Loads a single micro-frontend’s configuration.
* **[ConfigurationService](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#configuration-service)** — **Shell scope**. Holds the platform-wide configuration shared across every micro-frontend.

These two are the only services used to read environment variables. In Angular the values are read through the `@onecx/angular-integration-interface` services; in React the same values are read through the `useConfiguration` hook of `@onecx/react-integration-interface` (see [React integration interface](../react/libraries/react-integration-interface.html)). Each section below shows the Angular and React usage side by side.

| |  {[AppStateService](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#app-state-service)} is **not** a configuration service. It carries runtime UI **state** (global error, global loading, current micro-frontend, current page, current location, current workspace, and authentication status). If a value is something the **deployment** decides — an endpoint, a feature flag, an auth URL — it belongs to AppConfigService or ConfigurationService, not to AppStateService. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#environment-variables-scopes)Choosing a scope

* Use **`AppConfigService`** for a value that belongs to a single application only.
* Use **`ConfigurationService`** for a value that must be visible to multiple applications, or that the Shell itself needs (authentication, theme, base URLs, platform feature flags).

The same variable may exist in both scopes; they do not overlap automatically, so place each value where it is actually needed.

## [](#environment-variables-mfe)Reading an application’s values (`AppConfigService`)

An application’s environment variables come from an `env.json` file that the build serves as a static asset.

### [](#environment-variables-mfe-provide)Making the values present

The major requirement is that an `env.json` file is **available to be fetched** by the application at runtime — `AppConfigService` reads its values from that file, so without it there is nothing to read. See [AppConfigService](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#app-config-service) for the full mechanics of how the service fetches the file.

1. Create `src/assets/env.json` in the application. The file is a JSON object of string keys and string values:

Example `src/assets/env.json`

```json
{
  "API_URL": "https://api.example.com",
  "SEARCH_BASE_URL": "https://search.example.com",
  "ENABLE_DARK_MODE": "true"
}
```

1. The Angular build copies `src/assets/` to the build output, so the file is available at `{baseUrl}/assets/env.json` at runtime. Because the file is a **deployment artifact**, it can be produced or rewritten at deploy time (for example by a container entrypoint that substitutes deployment-specific values).
2. `AppConfigService` reads the file from `{baseUrl}/assets/env.json`, so the path must resolve from the application’s own base URL.

### [](#environment-variables-mfe-read)Reading the values

The values in `env.json` are the same regardless of framework; only the way they are read differs. Angular reads them with the `AppConfigService` injectable, React with the `useConfiguration` hook.

#### [](#environment-variables-mfe-read-angular)Angular

`AppConfigService` is a plain `@Injectable()` (not provided in root), so the application provides it and calls `init(baseUrl)` once during bootstrap. Rather than hard-coding the base URL, read it from {[AppStateService](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#app-state-service)}: the current micro-frontend’s `remoteBaseUrl` is the base path under which the application is mounted, and it is exactly what `init()` needs to locate `{baseUrl}/assets/env.json`.

Example `src/app/app.config.ts`

```ts
import { inject, provideAppInitializer } from '@angular/core';
import {
  AppConfigService,
  AppStateService,
} from '@onecx/angular-integration-interface';
import { firstValueFrom } from 'rxjs';

export function appConfigServiceInitializer(
  appStateService: AppStateService,
  appConfigService: AppConfigService,
) {
  return async () => {
    const mfe = await firstValueFrom(appStateService.currentMfe$.asObservable());
    await appConfigService.init(mfe.remoteBaseUrl);
  };
}

// In the application's providers:
// provideAppInitializer(() =>
//   appConfigServiceInitializer(
//     inject(AppStateService),
//     inject(AppConfigService),
//   )(),
// ),
```

Once `init()` has completed, values are read synchronously:

Example `src/app/my-feature.component.ts`

```ts
const apiUrl = this.appConfigService.getProperty('API_URL');
const allValues = this.appConfigService.getConfig();
```

See [AppConfigService](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#app-config-service) for the full API.

#### [](#environment-variables-mfe-read-react)React

The `@onecx/react-integration-interface` has no separate app-config hook — the same `useConfiguration` hook reads the application’s `env.json`. The `ConfigurationProvider` loads that file on mount (from `assets/env.json` by default), so the application only needs to wrap itself in the provider once and read the values from the hook. Application-specific keys (those not in `CONFIG_KEY`) are read from the `config` snapshot:

Example `src/MyFeature.tsx`

```tsx
import {
  ConfigurationProvider,
  useConfiguration,
} from '@onecx/react-integration-interface';

// Wrap the application once, at the root:
// <ConfigurationProvider>
//   <MyApp />
// </ConfigurationProvider>

const MyFeature = () => {
  const { config } = useConfiguration();
  const apiUrl = config?.API_URL; // value read from env.json
  return <div>API URL: {apiUrl ?? 'loading…'}</div>;
};
```

`useConfiguration` also exposes async `getProperty(key)` and `getConfig()` for programmatic reads. See [Configuration Provider](../react/libraries/react-integration-interface.html#configuration-provider) for the full API.

## [](#environment-variables-shell)Applying changes to the Shell at deployment (`ConfigurationService`)

The Shell’s environment variables are supplied as **deployment-time environment variables** of the Shell container. The Shell UI container writes those values into its own `assets/env.json` at startup, and `ConfigurationService` loads them from there. This is how you apply changes to the Shell without rebuilding the application code.

### [](#environment-variables-shell-provide)Making the Shell values present

Set the required values as environment variables on the Shell deployment. The container injects them into the Shell’s `assets/env.json` at startup.

Example Shell environment variables

```dockerfile
ENV APP_BASE_HREF /newShell/
ENV KEYCLOAK_URL http://keycloak:8080/
ENV AUTH_SERVICE keycloak
ENV ONECX_PORTAL_SEARCH_BUTTONS_REVERSED 'false'
```

Because `ConfigurationService` is **owned by the Shell**, micro-frontends never initialise it. They read its values through the same API, so any change applied to the Shell is picked up by every application that reads it.

### [](#environment-variables-shell-read)Reading the Shell values

Shell values are read asynchronously: the value is only available once the Shell has initialised its configuration, so reads use `await` in every framework. For the well-known platform keys, use the `CONFIG_KEY` enum rather than ad-hoc strings.

#### [](#environment-variables-shell-read-angular)Angular

Import `CONFIG_KEY` and `ConfigurationService` from `@onecx/angular-integration-interface`:

Example `src/app/keycloak-banner.component.ts`

```ts
import {
  CONFIG_KEY,
  ConfigurationService,
} from '@onecx/angular-integration-interface';

const keycloakUrl = await this.configurationService.getProperty(CONFIG_KEY.KEYCLOAK_URL);
const allValues = await this.configurationService.getConfig();
```

See [ConfigurationService](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#configuration-service) for the full API.

#### [](#environment-variables-shell-read-react)React

The Shell reads its own `env.json` through the same `useConfiguration` hook — there is no separate app-config hook in React. Read a platform value with the async `getProperty`, gated on the provider’s `isInitialized` promise so the value has been loaded first:

Example `src/KeycloakBanner.tsx`

```tsx
import { useEffect, useState } from 'react';
import {
  CONFIG_KEY,
  useConfiguration,
} from '@onecx/react-integration-interface';

const KeycloakBanner = () => {
  const { getProperty, isInitialized } = useConfiguration();
  const [keycloakUrl, setKeycloakUrl] = useState<string | undefined>();

  useEffect(() => {
    void isInitialized.then(async () => {
      setKeycloakUrl(await getProperty(CONFIG_KEY.KEYCLOAK_URL));
    });
  }, [getProperty, isInitialized]);

  return keycloakUrl ? <a href={keycloakUrl}>SSO</a> : null;
};
```

The React `CONFIG_KEY` enum is a subset of the Angular one, so only the platform keys shared by both frameworks are available. See [Configuration Provider](../react/libraries/react-integration-interface.html#configuration-provider) for the full API.

### [](#environment-variables-shell-config-keys)Available Shell configuration variables

`CONFIG_KEY` declares the platform variables the Shell defines and that `ConfigurationService` can return. Only the variables the Shell and the OneCX libraries actually read today are listed below; the remaining members of the `CONFIG_KEY` enum are kept for compatibility but are not currently read by the Shell or the libraries.

| Key                                                                                     |
| --------------------------------------------------------------------------------------- |
| Type                                                                                    |
| Purpose                                                                                 |
| APP\_BASE\_HREF                                                                         |
| string                                                                                  |
| The base path (Angular baseHref) the Shell is served under; used to build Shell routes. |
| KEYCLOAK\_REALM                                                                         |
| string                                                                                  |
| Keycloak realm name.                                                                    |
| KEYCLOAK\_URL                                                                           |
| string                                                                                  |
| Base URL of the Keycloak server.                                                        |
| KEYCLOAK\_CLIENT\_ID                                                                    |
| string                                                                                  |
| Keycloak client id.                                                                     |
| KEYCLOAK\_ENABLE\_SILENT\_SSO                                                           |
| boolean                                                                                 |
| Whether silent single-sign-on is enabled.                                               |
| KEYCLOAK\_TIME\_SKEW                                                                    |
| number                                                                                  |
| Allowed token time skew, in seconds.                                                    |
| KEYCLOAK\_UPDATE\_TOKEN\_MIN\_VALIDITY                                                  |
| number                                                                                  |
| Minimum token validity (seconds) before a silent token refresh is triggered.            |
| KEYCLOAK\_ON\_TOKEN\_EXPIRED\_ENABLED                                                   |
| boolean                                                                                 |
| Whether the onTokenExpired handler is active.                                           |
| KEYCLOAK\_ON\_AUTH\_REFRESH\_ERROR\_ENABLED                                             |
| boolean                                                                                 |
| Whether the onAuthRefreshError handler is active.                                       |
| AUTH\_SERVICE                                                                           |
| string                                                                                  |
| Authentication service to use (for example keycloak).                                   |
| AUTH\_SERVICE\_CUSTOM\_URL                                                              |
| string                                                                                  |
| URL of a custom authentication remote module (Module Federation).                       |
| AUTH\_SERVICE\_CUSTOM\_MODULE\_NAME                                                     |
| string                                                                                  |
| Exposed module name of the custom authentication remote.                                |
| CUSTOM\_AUTH\_SHARE\_SCOPE                                                              |
| string                                                                                  |
| Module Federation share scope used when loading the custom authentication remote.       |
| ONECX\_PORTAL\_SEARCH\_BUTTONS\_REVERSED                                                |
| boolean                                                                                 |
| Whether the search buttons are reversed.                                                |
| APP\_VERSION                                                                            |
| string                                                                                  |
| The application version reported by the Shell.                                          |
| IS\_SHELL                                                                               |
| boolean                                                                                 |
| Marker that identifies the running application as the Shell.                            |
| POLYFILL\_SCOPE\_MODE                                                                   |
| string                                                                                  |
| Polyfill scope mode (PERFORMANCE or PRECISION) used when loading dynamic styles.        |

## [](#environment-variables-troubleshooting)Troubleshooting

### [](#environment-variables-troubleshooting-404)`GET …​/assets/env.json` returns 404

* Confirm `src/assets/env.json` exists in the source and is included in the build output.
* Confirm the file is reachable at the expected path: `{baseUrl}/assets/env.json` for the application, the Shell’s own `assets/env.json` for the Shell.
* If the file is produced at deploy time, confirm the deployment step actually wrote it next to the running application.

### [](#environment-variables-troubleshooting-not-applied)Configuration is not applied

* `AppConfigService` must be initialised (with the correct base URL) before values are read.
* `ConfigurationService` is initialised by the Shell, not by applications. If a value is missing, check the Shell deployment’s environment variables, not the application.
* Values are string key/value pairs. Confirm the key spelling and that the value is a string.

## [](#related)Related

* [AppConfigService](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#app-config-service) — application-scope runtime configuration (MFE `env.json`).
* [ConfigurationService](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#configuration-service) — Shell-scope runtime configuration (platform-wide).
* [AppStateService](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#app-state-service) — runtime UI state (not configuration).
* [React integration interface](../react/libraries/react-integration-interface.html) — React equivalents for reading these values.
