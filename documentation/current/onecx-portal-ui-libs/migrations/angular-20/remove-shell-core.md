# Remove @onecx/shell-core

In version 7 of the libraries, the `@onecx/shell-core` package has been removed. Shell layout components and `WorkspaceConfigBffService` have been moved to the `shell-ui` application. All `@onecx/shell-core` imports and any related usage must be removed from your application.

**Actions**

* Uninstall the deprecated package:

```bash
npm uninstall --save @onecx/shell-core
```

* Remove all imports and usage from the project

| |  The moved components and services are now provided directly by the shell‑ui application and should be consumed from there. |
| ----------------------------------------------------------------------------------------------------------------------------- |
