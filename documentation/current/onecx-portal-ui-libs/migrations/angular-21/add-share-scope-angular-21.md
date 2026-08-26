# Set shareScope values in Helm

After migration to Angular 21, add a `shareScope` field per microfrontend spec entry in your Helm values.

## [](#%5Frequired%5Fchange)Required change

Set `shareScope` based on app technology:

```yaml
shareScope: angular_21  # for Angular MFEs
shareScope: react_21    # for React MFEs
```

Add this field in the microfrontend properties for each exposed entry (for example in `helm/values.yaml` under `app.operator.microfrontend.specs.<entry>`).

Example:

```yaml
app:
  operator:
    microfrontend:
      specs:
        main:
          exposedModule: ./OneCXThemeModule
          shareScope: angular_21
        theme-data:
          exposedModule: ./OneCXThemeDataComponent
          shareScope: angular_21
        theme-logo:
          exposedModule: ./OneCXCurrentThemeLogoComponent
          shareScope: angular_21
```

| |  A strict and consistent shareScope value allows Angular 21 applications to share Angular 21 package instances across host and remotes. Use exactly the same value across connected apps of the same technology/runtime. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
