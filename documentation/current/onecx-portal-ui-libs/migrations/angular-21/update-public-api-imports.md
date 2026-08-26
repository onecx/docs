# Update imports to supported public APIs

OneCX v8 contains multiple public API export updates across libraries. To avoid compile errors after upgrading, ensure your imports use package entry points and currently exported symbols.

## [](#%5Fexample)Example

Before

```typescript
import { AuthServiceWrapper } from '@onecx/angular-auth/src/lib/auth-service-wrapper'
```

After

```typescript
import { AuthServiceWrapper } from '@onecx/shell-auth'
```
