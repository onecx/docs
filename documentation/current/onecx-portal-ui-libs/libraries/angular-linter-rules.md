# angular-linter-rules

`@onecx/angular-linter-rules` is an ESLint plugin that provides opinionated Angular rules. It ships with a predefined config (`recommended`) which enables all rules with the severity `warn`.

## [](#installation)Installation

Install the plugin as a dev dependency:

```sh
npm i -D @onecx/angular-linter-rules
```

## [](#use-the-predefined-config-recommended)Use the predefined config (recommended)

The plugin exports an ESLint config named `recommended`. This is the easiest way to enable all rules in one step.

### [](#old-way-eslint-legacy-config-eslintrc)Old way: ESLint "legacy" config (`.eslintrc.*`)

Add the recommended config via `extends`:

```json
{
  "extends": ["plugin:@onecx/angular-linter-rules/recommended"]
}
```

You can place this in your workspace root `.eslintrc.json` or in a project-level `.eslintrc.json`.

### [](#new-way-eslint-flat-config-eslint-config)New way: ESLint flat config (`eslint.config.*`)

The exported `configs.recommended` is in the legacy ESLint config shape. For a flat config setup, you can still reuse the generated rule map from `configs.recommended.rules`.

```js
// eslint.config.cjs
const angularLinterRules = require('@onecx/angular-linter-rules')

module.exports = [
  {
    plugins: {
      '@onecx/angular-linter-rules': angularLinterRules.plugin,
    },
    rules: {
      ...angularLinterRules.configs.recommended.rules,
    },
  },
]
```

## [](#what-recommendedrules-means)What `recommendedRules` means

Internally, the `recommended` config uses `recommendedRules`.`recommendedRules` is generated from the plugin’s exported `rules` object and sets every rule to `"warn"`.

That means:

* When a new rule is added to `@onecx/angular-linter-rules`, it is automatically included in `recommended`.
* All rules are enabled under the rule namespace `@onecx/angular-linter-rules/<rule-name>`.

Example rule keys:

* `@onecx/angular-linter-rules/no-subscribe-assignment`
* `@onecx/angular-linter-rules/no-translate-instant`
* `@onecx/angular-linter-rules/prefer-translate-params`

## [](#override-severities-or-disable-specific-rules)Override severities or disable specific rules

You can override any rule after extending the config:

```json
{
  "extends": ["plugin:@onecx/angular-linter-rules/recommended"],
  "rules": {
    "@onecx/angular-linter-rules/no-subscribe-assignment": "error",
    "@onecx/angular-linter-rules/no-translate-instant": "off"
  }
}
```

For flat config, override rules after spreading `configs.recommended.rules`:

```js
// eslint.config.cjs
const angularLinterRules = require('@onecx/angular-linter-rules')

module.exports = [
  {
    plugins: {
      '@onecx/angular-linter-rules': angularLinterRules.plugin,
    },
    rules: {
      ...angularLinterRules.configs.recommended.rules,
      '@onecx/angular-linter-rules/no-subscribe-assignment': 'error',
      '@onecx/angular-linter-rules/no-translate-instant': 'off',
    },
  },
]
```
