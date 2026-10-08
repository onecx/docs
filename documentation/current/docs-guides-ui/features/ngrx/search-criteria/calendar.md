# Calendar

## [](#goal)Goal: Add Calendar Input

Add a Calendar as a search criteria input field for your search page.

| |  Please replace all occurences of **exampleDate** with the actual name in the following code snippets |
| ------------------------------------------------------------------------------------------------------- |

## [](#parameters)1\. Parameters

First add a new member to the <%= featurePropertyName %>SearchCriteriasSchema:

_Adapt in File:_ `<feature>-search.parameters.ts`

```javascript
    exampleDate: z
        .string()
        .transform((v) => (v ? new Date(v) : undefined))
        .optional(),
```

## [](#html)2\. HTML

Next, add the following code to your formGroup in the html file and adapt:

* by replacing all occurences of `exampleDate` with the actual name which is defined
* `dateFormat` according to your requirements following this primeng specific date format <https://primeng.org/calendar#format> where `mm/dd/yy` is the default.

_Adapt in File:_ `<feature>-search.component.html`

```html
    <span class="p-float-label">
        <p-calendar
            id="exampleDate"
            formControlName="exampleDate"
            name="exampleDate"
            ngDefaultControl
            pInputDate
            type="text"
            appendTo="body"
            [showClear]="true"
            dateFormat="" <-- SPECIFY THE REQUIRED DATE FORMAT OR REMOVE THIS PROPERTY IF DEFAULT SHOULD BE USED
            >
        </p-calendar>
        <label for="exampleDate">{{
            'YOUR_PRODUCT_SEARCH.CRITERIA.ID' | translate
        }}</label>
    </span>
```

| |  Make sure to include the appendTo="body" property in the p-calendar component, otherwise the calendar could be rendered incorrectly and cause layout issues. |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#selectors)3\. Selectors

Furthermore, the following needs to be done to correctly create date strings out of a p-calendar selector:

_Adapt in File:_ `<feature>-search.component.ts`

```javascript
    import { Calendar } from 'primeng/calendar';
    ...

    @ViewChildren(Calendar) calendars!: QueryList<Calendar>;
    ...

    search(formValue: FormGroup) {
      const searchCriteria = buildSearchCriteria(
        formValue.getRawValue(),
        this.calendars, <-- ADD THIS LINE
        {
            removeNullValues: true,
        },
      );
      this.store.dispatch(
      <%= featureClassName %>SearchActions.searchButtonClicked({ searchCriteria }),
      );
    }
```

## [](#effects)4\. Effects (Optional)

If it is required to only have the `date` and not the `` datetime' in the URL, you need to adapt the `syncParamsToUrl$ `` effect:

_Adapt in File:_ `<feature>-search.effects.ts`

```javascript
  syncParamsToUrl$ = createEffect(
    () => {
      return this.actions$.pipe(
        ofType(
          <%= featureClassName %>SearchActions.searchButtonClicked,
          <%= featureClassName %>SearchActions.resetButtonClicked,
        ),
        concatLatestFrom(() => [
          this.store.select(<%= featurePropertyName %>SearchSelectors.selectCriteria),
          this.route.queryParams,
        ]),
        tap(([, criteria, queryParams]) => {
          const results =
            <%= featurePropertyName %>SearchCriteriasSchema.safeParse(queryParams);
          if (!results.success || !equal(criteria, results.data)) {
            const params = {
              ...criteria,
              exampleDate: criteria.exampleDate?.toISOString()?.slice(0, 10) <-- ADD THIS LINE TO ONLY HAVE THE DATE IN THE URL
            };
            this.router.navigate([], {
              relativeTo: this.route,
              queryParams: params,
              replaceUrl: true,
              onSameUrlNavigation: 'ignore',
            });
          }
        }),
      );
    },
    { dispatch: false },
  );
```

| |  Don’t forget to add the translations to your **de.json** and **en.json**. |
| ---------------------------------------------------------------------------- |
