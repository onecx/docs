# ESM bundling awareness (prerequisite)

In OneCX v8, `@onecx/accelerator` and `@onecx/integration-interface` are published as ES modules.

For standard Angular application builds, this is usually non-breaking. This page helps you quickly detect and fix issues in custom runtime/build setups.

## [](#%5Fwhat%5Fchanged)What changed

* Packages are ESM (`"type": "module"`).
* CommonJS-only usage patterns (for example `require()` in custom Node scripts) may need adaptation.

## [](#%5Fwhen%5Fto%5Fcheck%5Fthis)When to check this

Check this prerequisite if your project includes custom scripts/tooling such as:

* Node scripts importing OneCX packages directly
* Custom webpack/rspack wrappers around MF runtime loading
* Test/dev scripts running outside Angular CLI/Nx standard build flow

## [](#%5Ftypical%5Fissues%5Fyou%5Fmight%5Fface)Typical issues you might face

* `ERR_REQUIRE_ESM`
* `require is not defined in ES module scope`
* Module resolution/import errors in custom scripts after dependency update

## [](#%5Fsolutions)Solutions

### [](#%5F1%5Freplace%5Frequire%5Fwith%5Fesm%5Fimports)1) Replace `require()` with ESM imports

Before

```javascript
const { EventsTopic } = require('@onecx/integration-interface')
```

After

```typescript
import { EventsTopic } from '@onecx/integration-interface'
```

### [](#%5F2%5Fensure%5Fscriptmodule%5Fruntime%5Fsupports%5Fesm)2) Ensure script/module runtime supports ESM

* Use an ESM-capable Node runtime and script configuration.
* Keep host and remotes on consistent dependency/runtime expectations.

### [](#%5F3%5Fif%5Fno%5Fcustom%5Fruntime%5Fusage%5Fexists)3) If no custom runtime usage exists

No action is needed. Treat this as awareness-only and continue with migration steps.
