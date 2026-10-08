# Dropdown

## [](#goal)Goal: Add Dropdown Input

Add a Dropdown as a search criteria input field for your search page.

| |  Please replace all occurences of **exampleEnum** with the actual name in the following code snippets |
| ------------------------------------------------------------------------------------------------------- |

## [](#parameters)1\. Parameters

First, add a new member to the <%= featurePropertyName %>SearchCriteriasSchema:

_Adapt in File:_ `<feature>-search.parameters.ts`

```javascript
    exampleEnum: z
        .string()
        .transform((v) => v as <%= featurePropertyName %>SearchRequestExampleEnum)
        .optional(),
```

## [](#html)2\. HTML

Next, add the following code to your formGroup in the html file and adapt by replacing all occurences of `exampleEnum` with the actual name which is defined.

_Adapt in File:_ `<feature>-search.component.html`

```html
    <span class="p-float-label">
        <p-dropdown
              id="exampleEnum"
              formControlName="exampleEnum"
              appendTo="body"
              [options]="(exampleEnum$ | async) ?? []"
              optionLabel="label"
              optionValue="value"
              placeholder="{{ 'YOUR_PRODUCT_SEARCH.CRITERIA.EXAMPLE_ENUM.PLACEHOLDER' | translate }}"
              display="chip"
              [showClear]="true"
        ></p-dropdown>
        <label for="exampleEnum$">{{
            'YOUR_PRODUCT_SEARCH.CRITERIA.EXAMPLE_ENUM.TITLE' | translate
        }}</label>
    </span>
```

## [](#component)3\. Component

Furthermore, the following needs to be done to have the correct translations displayed:

_Adapt in File:_ `<feature>-search.component.ts`

```javascript
    import { TranslateService } from '@ngx-translate/core';
    import { enumToDropdownOptions } from '@onecx/angular-accelerator';
    ...

    constructor(
        ...
        private translateService: TranslateService,
        ...
    ) {}
    ...

    exampleEnum$ = enumToDropdownOptions(
        this.translateService,
        <%= featurePropertyName %>SearchRequestExampleEnum,
        'YOUR_PRODUCT_SEARCH.CRITERIA.EXAMPLE_ENUM.OPTIONS.',
    );
```

| |  Don’t forget to add the translations to your **de.json** and **en.json**. |
| ---------------------------------------------------------------------------- |
