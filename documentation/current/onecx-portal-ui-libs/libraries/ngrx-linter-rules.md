# ngrx-linter-rules

`@onecx/ngrx-linter-rules` is an ESLint plugin that provides opinionated NgRx rules. It ships with a predefined config (`recommended`) which enables all rules with the severity `warn`.

## [](#installation)Installation

Install the plugin as a dev dependency:

```sh
npm i -D @onecx/ngrx-linter-rules
```

## [](#use-the-predefined-config-recommended)Use the predefined config (recommended)

The plugin exports an ESLint config named `recommended`. This is the easiest way to enable all rules in one step.

### [](#old-way-eslint-legacy-config-eslintrc)Old way: ESLint "legacy" config (`.eslintrc.*`)

Add the recommended config via `extends`:

```json
{
  "extends": ["plugin:@onecx/ngrx-linter-rules/recommended"]
}
```

You can place this in your workspace root `.eslintrc.json` or in a project-level `.eslintrc.json`.

### [](#new-way-eslint-flat-config-eslint-config)New way: ESLint flat config (`eslint.config.*`)

The exported `configs.recommended` is in the legacy ESLint config shape. For a flat config setup, you can still reuse the generated rule map from `configs.recommended.rules`.

```js
// eslint.config.cjs
const ngrxLinterRules = require('@onecx/ngrx-linter-rules')

module.exports = [
  {
    plugins: {
      '@onecx/ngrx-linter-rules': ngrxLinterRules.plugin,
    },
    rules: {
      ...ngrxLinterRules.configs.recommended.rules,
    },
  },
]
```

## [](#what-recommendedrules-means)What `recommendedRules` means

Internally, the `recommended` config uses `recommendedRules`.`recommendedRules` is generated from the plugin’s exported `rules` object and sets every rule to `"warn"`.

That means:

* When a new rule is added to `@onecx/ngrx-linter-rules`, it is automatically included in `recommended`.
* All rules are enabled under the rule namespace `@onecx/ngrx-linter-rules/<rule-name>`.

Example rule keys:

* `@onecx/ngrx-linter-rules/no-store-dispatch-in-effect`
* `@onecx/ngrx-linter-rules/http-calls-only-in-effects`

## [](#override-severities-or-disable-specific-rules)Override severities or disable specific rules

You can override any rule after extending the config:

```json
{
  "extends": ["plugin:@onecx/ngrx-linter-rules/recommended"],
  "rules": {
    "@onecx/ngrx-linter-rules/no-store-dispatch-in-effect": "error",
    "@onecx/ngrx-linter-rules/http-calls-only-in-effects": "off"
  }
}
```

For flat config, override rules after spreading `configs.recommended.rules`:

```js
// eslint.config.cjs
const ngrxLinterRules = require('@onecx/ngrx-linter-rules')

module.exports = [
  {
    plugins: {
      '@onecx/ngrx-linter-rules': ngrxLinterRules.plugin,
    },
    rules: {
      ...ngrxLinterRules.configs.recommended.rules,
      '@onecx/ngrx-linter-rules/no-store-dispatch-in-effect': 'error',
      '@onecx/ngrx-linter-rules/http-calls-only-in-effects': 'off',
    },
  },
]
```
