# Update Theme Service usage

In OneCX v6, onecx-shell is responsible for loading and applying the theme globally for the chosen `workspace`. See [OneCX Theming Guide](https://onecx.github.io/docs/documentation/current/docs-guides-ui/angular/theming.html) for more information.

The `ThemeService` now only exposes the `currentTheme$` property of type CurrentThemeTopic from the `@onecx/integration-interface` library. All previous theme-loading logic has been removed from the service.

## [](#%5Fremove%5Fdeprecated%5Fthemeservice%5Fmembers)Remove deprecated ThemeService members

* Remove `baseUrlV1` property usages
* Remove `getThemeRef()` function calls
* Remove `loadAndApplyTheme()` function calls
* Remove `apply()` function calls

| |  These members no longer exist in ThemeService. You only need to remove calls or references to them in your application code. |
| ------------------------------------------------------------------------------------------------------------------------------- |

In case your App applies the theme temporarily for preview purposes only, use the `apply()` function implementation provided below:

Apply

```typescript
async function apply(themeService: ThemeService, theme: Theme): Promise<void> {
  await themeService.currentTheme$.publish(theme)
  if (theme.properties) {
    for (const group of Object.values(theme.properties)) {
      for (const [key, value] of Object.entries(group)) {
        document.documentElement.style.setProperty(`--${key}`, value)
      }
    }
  }
}
```
