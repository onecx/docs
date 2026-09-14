# Application Setup

Make sure that the application is set up correctly to work in the environment. Review the required setup steps in [Required Setup](../setup/required/index.html) first. Regardless of the used local development strategy, the following should be checked:

* `exposedModule` is set to the correct module name
* `tagName` is set to the correct tag name
* `remoteEntry` url is set to the correct url
* `shareScope` is set to the correct share scope for the app configuration (some apps will not work correctly without it, e.g. an app using a newer Angular major version than the shell’s default share scope)

Depending on the used local development strategy, those values should be set in different places (data imports for the local environment, `values.yaml` of the application, or manual configuration on the OneCX platform via the Application Store and Workspace UIs).

## [](#remote-entry-url)Remote entry URL

Verify that the configured `remoteEntry` URL matches the URL where the app is actually running and that `remoteEntry.js` is directly reachable there. For example, if the app is expected at `<http://localhost:4200>`, open `<http://localhost:4200/remoteEntry.js>` in the browser or request it directly and confirm that it loads successfully.

The setup and expected local URL are described in [Expose a Remote Module](../setup/required/expose-remote-module.html).

## [](#remote-module-name)Remote module name

Verify that the remote module name in your module federation configuration (`module-federation.config.js` or `webpack.config.js`, depending on your setup) is the same as the remote module setting in the Application Store.

Navigate to the Application Store → open the app → click on the 'Components' tab → open the 'Module' UI component → check the app ID:

__Table 1\. Example module federation configuration and Application Store setting (remote module name)__
| module-federation.config.js                                                                                                                                                                   | Application Store                                                                            |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| ... const config = withModuleFederationPlugin({   name: 'onecx-workspace-ui',   filename: 'remoteEntry.js',   exposes: {     './OneCXWorkspaceModule': 'src/main.ts',     ...     }   }), ... | ![application store remote module name](../_images/application_store_remote_module_name.png) |

## [](#tag-name)Tag name

Verify that the tag name for the component is the same as the tag name set in the Application Store:

__Table 2\. Example values.yaml and Application Store setting (tag name)__
| values.yaml                                                                                                                                                                                                                                                                                                                                                                                                                        | Application Store                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| ... microfrontend:   enabled: true   specs:     main:       exposedModule: "./OneCXWorkspaceModule"       description: "OneCX Workspace UI"       note: "OneCX Workspace UI auto import via MF operator"       type: MODULE       technology: WEBCOMPONENTMODULE       remoteName: onecx-workspace       tagName: ocx-workspace-component       endpoints:         \- name: workspace-detail           path: /{workspace-name} ... | ![application store remote module tag name](../_images/application_store_remote_module_tag-name.png) |

## [](#share-scope)Share scope

Verify that the app (and, where applicable, its individual microfrontends) is assigned to the correct `shareScope`. Not every app requires an explicit `shareScope`, but some configurations will not work correctly without it — for example, an app that must be shared under a specific Angular major version’s scope rather than the shell’s `default` scope.

Example `values.yaml` share scope configuration

```yaml
app:
    operator:
        microfrontend:
            spec:
                shareScope: 'angular_21' # this app should be loaded into the 'angular_21' share scope
```

See [Share Scopes](../setup/required/configure-remote-package-sharing.html#share-scopes) for the full explanation of how share scopes are assigned and which scope an application should use.
