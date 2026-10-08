# AutoComplete for suggestions with array of type string

## [](#goal)Goal: Add AutoComplet String

Add an AutoComplete for suggestions with array of type string as a search criteria input field for your search page.

## [](#parameters)1\. Parameters

Please define the member for your **<%= featurePropertyName %>SearchCriteriasSchema** here

| |  Please replace all occurences of **exampleStringArray** with the actual name in the following code snippets. |
| --------------------------------------------------------------------------------------------------------------- |

_Adapt in File:_ `<feature>-search.parameters.ts`

```javascript
    exampleStringArray: z
        .union([z.string(), z.array(z.string())])
        .transform((v: string | string[] | undefined): string[] | undefined =>
        v instanceof Array || !v
            ? (v as string[] | undefined)
            : ([v] as string[]),
        )
        .transform((v: string[] | undefined) => v?.map((e) => e))
        .optional(),
```

## [](#state-and-viewmodel)2\. State & viewmodel

Add additional array member for the autocomplete suggestions in your state and viewmodel:

_Adapt in Files:_ `<feature>-search.viewmodel.ts` and `<feature>-search.state.ts`

```javascript
...
    exampleStringArrayOptions: string[]
...
```

## [](#actions)3\. Actions

Create following actions to handle the events regarding autocomplete:

_Adapt in File:_ `<feature>-search.actions.ts`

```javascript
...
    events: {
        'exampleStringArray data text entered': props<{ exampleStringArrayInputValue: string }>(),
        'exampleStringArray data received ': props<{ exampleStringArrayOptions: string[] }>(),
        'exampleStringArray data loading failed': emptyProps(),
        'exampleStringArray selected': props<{ selectedExampleStringArrayValue: string }>(),
        'exampleStringArray unselected': props<{ unSelectedExampleStringArrayValue: string }>(),
    },
...
```

## [](#html)4\. HTML

Add the following code to your formGroup in the html file:

_Adapt in File:_ `<feature>-search.component.html`

```html
    <span class="p-float-label">
        <p-autoComplete
            id="exampleStringArray"
            formControlName="exampleStringArray"
            (completeMethod)="searchExampleStringArrayData($event)"
            [suggestions]="vm?.exampleStringArrayOptions ?? []"
            [forceSelection]="true"
            [multiple]="true" <-- ONLY NECESSARY IF MULTIPLE VALUES CAN BE SELECTED
            [showEmptyMessage]="true"
            [emptyMessage]="
            vm?.exampleStringArrayOptions?.length === 0
                ? ('YOUR_PRODUCT_SEARCH.CRITERIA.EXAMPLE_ID_NOT_FOUND' | translate)
                : ''
            "
            (onSelect)="selectExampleStringArrayValue($event)"
            (onUnselect)="unSelectExampleStringArrayValue($event)"
        >
        </p-autoComplete>
        <label for="exampleStringArray">{{
            'YOUR_PRODUCT_SEARCH.CRITERIA.ID' | translate
        }}</label>
    </span>
```

## [](#component)5\. Component

Add the respective methods to handle the different events:

_Adapt in File:_ `<feature>-search.component.ts`

```javascript
...
    searchExampleStringArrayData(event: AutoCompleteCompleteEvent) {
      this.store.dispatch(
        <feature>SearchActions.exampleStringArrayDataTextEntered({
            exampleStringArrayInputValue: event.query,
        }),
      );
    }

    selectExampleStringArrayValue(event: AutoCompleteSelectEvent) {
      this.store.dispatch(
        <feature>SearchActions.exampleStringArraySuggestionSelected({
            selectedExampleStringArrayValue: event.value,
        }),
      );
    }

    unSelectExampleStringArrayValue(event: AutoCompleteUnselectEvent) {
      this.store.dispatch(
        <feature>SearchActions.exampleStringArraySuggestionUnselected({
            unSelectedExampleStringArrayValue: event.value,
        }),
      );
    }
...
```

## [](#reducers)6\. Reducers

In the reducers file you need to define the functions:

_Adapt in File:_ `<feature>-search.reducers.ts`

```javascript
...
  on(
    <%= featureClassName %>SearchActions.exampleStringArrayDataReceived,
    (state: <%= featureClassName %>SearchState, { exampleStringArrayOptions }): <%= featureClassName %>SearchState => ({
      ...state,
      exampleStringArrayOptions: exampleStringArrayOptions,
    }),
  ),
  on(
    <%= featureClassName %>SearchActions.exampleStringArrayDataLoadingFailed,
    (state: <%= featureClassName %>SearchState): <%= featureClassName %>SearchState => ({
      ...state,
      exampleStringArrayOptions: [],
    }),
  ),
  on(
    <%= featureClassName %>SearchActions.exampleStringArraySuggestionSelected,
    (
      state: <%= featureClassName %>SearchState,
      { selectedExampleStringArrayValue },
    ): <%= featureClassName %>SearchState => {
      const isValuePresent =
        state.exampleStringArraySelectedValues.includes(selectedExampleStringArrayValue);
      return {
        ...state,
        exampleStringArraySelectedValues: isValuePresent
          ? state.exampleStringArraySelectedValues
          : [...state.exampleStringArraySelectedValues, selectedExampleStringArrayValue],
        exampleStringArrayOptions: [],
      };
    },
  ),
  on(
    <%= featureClassName %>SearchActions.exampleStringArraySuggestionUnselected,
    (
      state: <%= featureClassName %>SearchState,
      { unSelectedExampleStringArrayValue },
    ): <%= featureClassName %>SearchState => ({
      ...state,
      exampleStringArraySelectedValues: state.exampleStringArraySelectedValues.filter(
        (exampleStringArray) => exampleStringArray !== unSelectedExampleStringArrayValue,
      ),
      exampleStringArrayOptions: [],
    }),
  ),
...
```

## [](#selectors)7\. Selectors

Add the missing selectors:

_Adapt in File:_ `<feature>-search.selectors.ts`

```javascript
...
    export const select<%= featureClassName %>SearchViewModel = createSelector(
      ...
      <feature>SearchSelectors.
      selectExampleStringArrayOptions,
      ...
      (
        ...
        exampleStringArrayOptions,
        ...
      ): <%= featureClassName %>SearchViewModel => ({
        ...
        exampleStringArrayOptions,
        ...
      }),
    );
...
```

## [](#effects)8\. Effects

Create the effect for getting the suggestions

_Adapt in File:_ `<feature>-search.effects.ts`

```javascript
...
    searchExampleStringArray$ = createEffect(() =>
      this.actions$.pipe(
        ofType(<%= featureClassName %>SearchActions.exampleStringArrayDataTextEntered),
        mergeMap((action) => {
          return this.<feature>Service
            .searchExampleStringArray(action.exampleStringArrayInputText)
            .pipe(
              map((response) =>
                <%= featureClassName %>SearchActions.exampleStringArrayDataReceived({
                  exampleStringArrayOptions: response.exampleStringArray, <-- NAME OF THE MEMBER WHICH IS DEFINED IN THE RESPONSE OBJECT
                }),
              ),
              catchError(() =>
                of<%= featureClassName %>SearchActions.exampleStringArrayDataLoadingFailed()),
              ),
            );
        }),
      ),
    );
...
```

| |  Don’t forget to add the translations to your **de.json** and **en.json**. |
| ---------------------------------------------------------------------------- |
