# Update ConfigurationService Usage

In OneCX v6, three methods of `ConfigurationService` have been updated to be asynchronous, returning `Promise` results instead of synchronous values.

## [](#%5Fupdate%5Fthe%5Ffollowing%5Fmethods)Update the following methods

* `getProperty(key)` → `await getProperty(key)`
* `getConfig()` → `await getConfig()`
* `setProperty(key, val)` → `await setProperty(key, val)`

Guidelines

* Update only methods of `ConfigurationService` imported from `@onecx/angular-integration-interface`.
* If inside an observable: wrap the call with `from(…​)` and use `switchMap` or `mergeMap`.
* Outside observables: use `await` in an `async` function; if `async` not allowed (e.g. `constructor`, `ngOnInit`), resolve the Promise with `.then(…​)`.
* Add `try/catch` for error handling where synchronous code previously assumed success.
* Update mocks to resolve promises:  
   * Jest → `jest.spyOn(service, 'getProperty').mockResolvedValue('val');`  
   * Jasmine → `spyOn(service, 'getConfig').and.returnValue(Promise.resolve(cfg));`

### [](#%5Fexample)Example

Before

```typescript
const theme = this.configService.getProperty(CONFIG_KEY.TKIT_PORTAL_DEFAULT_THEME);

const config = this.configService.getConfig();

this.configService.setProperty(CONFIG_KEY.APP_VERSION, '6.0.0');
```

After

```typescript
const theme = await this.configService.getProperty(CONFIG_KEY.TKIT_PORTAL_DEFAULT_THEME);

const config = await this.configService.getConfig();

await this.configService.setProperty(CONFIG_KEY.APP_VERSION, '6.0.0');
```

## [](#%5Fcustom%5Fauthservicefactory)Custom AuthServiceFactory

If your application provides a custom `AuthServiceFactory` (the `custom` option of `CONFIG_KEY.AUTH_SERVICE`), note the following:

* `AuthServiceWrapper` awaits the async configuration reads (e.g. `CONFIG_KEY.AUTH_SERVICE_CUSTOM_URL`) before loading the remote factory.
* The exported factory function itself may return an `AuthService` synchronously or a `Promise<AuthService>`; `AuthServiceWrapper` will await the factory result.
* The v6 injector callback always returns a `Promise` for both `CONFIG` and `KEYCLOAK_AUTH_SERVICE`. Any factory that uses the injector must be `async` and `await` the returned value; only a factory that does not use the injector can remain synchronous.
* The returned auth service must implement `init`, `getHeaderValues`, `logout`, and `updateTokenIfNeeded`.

### [](#%5Fexamples)Examples

#### [](#%5Fsynchronous%5Ffactory%5Fno%5Fchange%5Frequired)Synchronous factory (no change required)

Before

```typescript
// exports default a factory that returns the service synchronously
import { CustomAuthService } from './custom-auth.service';

export default function () {
  return new CustomAuthService();
}
```

After

```typescript
// unchanged: synchronous factories continue to work
import { CustomAuthService } from './custom-auth.service';

export default function () {
  return new CustomAuthService();
}
```

#### [](#%5Fasynchronous%5Ffactory%5Fawait%5Finjected%5Fconfiguration)Asynchronous factory (await injected configuration)

Before

```typescript
import type { Config } from '@onecx/integration-interface';
import { CustomAuthService } from './custom-auth.service';

const Injectables = {
  CONFIG: 'CONFIG',
  KEYCLOAK_AUTH_SERVICE: 'KEYCLOAK_AUTH_SERVICE'
} as const;

type Injectable = typeof Injectables[keyof typeof Injectables];
type Injector = (injectable: Injectable) => unknown;

export default function (injector: Injector) {
  // v5 injectors return CONFIG synchronously, so no await is needed here
  const cfg = injector(Injectables.CONFIG) as Config;
  return new CustomAuthService(cfg);
}
```

After

```typescript
// Make the factory async and await injected values when needed
import type { Config } from '@onecx/integration-interface';
import { CustomAuthService } from './custom-auth.service';

const Injectables = {
  CONFIG: 'CONFIG',
  KEYCLOAK_AUTH_SERVICE: 'KEYCLOAK_AUTH_SERVICE'
} as const;

type Injectable = typeof Injectables[keyof typeof Injectables];
type Injector = (injectable: Injectable) => Promise<unknown>;

export default async function (injector: Injector) {
  // v6 injectors may return a Promise for CONFIG; await it before using it
  const cfg = (await injector(Injectables.CONFIG)) as Config;
  // perform any async initialization here, then return the service
  return new CustomAuthService(cfg);
}
```
