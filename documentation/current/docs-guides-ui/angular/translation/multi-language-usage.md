# OneCX Multi-language Translations Usage

## [](#overview)Overview

This document provides guidance on how to use multi-language translations in a [**OneCX compatible**](../app-to-onecx.html) application after setting it up using the [multi-language setup document](multi-language-setup.html).

## [](#prerequisites)Prerequisites

Before proceeding, ensure that the multi-language setup is complete.

## [](#usage)Usage

It is possible to use functionalities from `@ngx-translate` library to implement translations in the application.

### [](#templates-usage)Templates Usage

Use translations via **translate** pipe.

component.html

```html
<p>{{ 'HELLO' | translate }}</p>
```

### [](#translate-service-usage)TranslateService Usage

Use translations via **TranslateService**.

component.ts

```typescript
import { TranslateService } from '@ngx-translate/core';

this.translate.get('WELCOME').subscribe((translated: string) => {
    console.log('Translated message:', translated);
});
```

### [](#with-parameters)With Parameters

Use translations with parameters. Example:

en.json

```json
{
  "GREETING": "Hello, {{name}}! Welcome back."
}
```

component.html

```html
<p>{{ 'GREETING' | translate:{ name: 'Alice' } }}</p>
```

component.ts

```typescript
import { TranslateService } from '@ngx-translate/core';
this.translate.get('GREETING', params).subscribe((translated: string) => {
    console.log('Translated with params:', translated);
});
```
