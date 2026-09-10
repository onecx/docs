# Configure Search Results

After generating the base search page, you need to configure how the search results are displayed to the user.  
The following actions must be taken.

## [](#action-s5)ACTION S5

If not yet done, specify the base entity properties in the OpenAPI specification, see [Create an Entity Schema](../create-schema.html).

## [](#action-s6)ACTION S6

Specify Columns in Result table

The next step is to configure the columns of the search results table. Here you can define which properties of your entity should be displayed in the results table, as well as their characteristics (e.g. if they are sortable or filterable).

### Template: Generated Search Result Columns

| Directory | <root-of-ui-app>/src/app/<feature>/pages/<resource>-search |
| --------- | ---------------------------------------------------------- |
| File      | <resource>-search.columns.ts                               |

ACTION S6 in `<resource>-search.columns.ts` 

```javascript
export const <resource>SearchColumns: DataTableColumn[] = [
  {
    columnType: ColumnType.STRING,
    id: 'changeMe',
    nameKey: '<RESOURCE>_SEARCH.RESULTS.CHANGE_ME',
    filterable: true,
    sortable: true,
    predefinedGroupKeys: [
      '<RESOURCE>_SEARCH.PREDEFINED_GROUP.DEFAULT',
      '<RESOURCE>_SEARCH.PREDEFINED_GROUP.EXTENDED',
      '<RESOURCE>_SEARCH.PREDEFINED_GROUP.FULL',
    ]
  }
  // ACTION S6: Define search results columns
];
```

Where **changeMe** is a column added to the `<Resource>SearchColumns`.

---

### Example: Book Search Result Columns

| Directory | bookstore/src/app/book/pages/book-search |
| --------- | ---------------------------------------- |
| File      | book-search.columns.ts                   |

Example: Book Search Result Columns 

```javascript
export const bookSearchColumns: DataTableColumn[] = [
  {
    columnType: ColumnType.STRING,
    id: 'bookTitle',
    nameKey: 'BOOK_SEARCH.RESULTS.BOOK_TITLE',
    filterable: true,
    sortable: true,
    predefinedGroupKeys: [
      'BOOK_SEARCH.PREDEFINED_GROUP.DEFAULT',
      'BOOK_SEARCH.PREDEFINED_GROUP.EXTENDED',
      'BOOK_SEARCH.PREDEFINED_GROUP.FULL',
    ]
  },
  {
    columnType: ColumnType.TRANSLATION_KEY,
    id: 'bookType',
    nameKey: 'BOOK_SEARCH.RESULTS.BOOK_TYPE',
    filterable: true,
    sortable: true,
    predefinedGroupKeys: [
      'BOOK_SEARCH.PREDEFINED_GROUP.FULL',
    ]
  }
  // ACTION S6: Define search results columns
]
```

Where **bookTitle** and **bookType** are columns added to the `BookSearchColumns`. The column **bookType** is only added to the predefined group **FULL**, so it will only be visible for users who select this group in the UI.

Refer to the [DataTableColumn overview](../../../onecx-portal-ui-libs/components/interactive-data-view/data-table-column.html) for more information.

## [](#action-s7)ACTION S7

Mapping from Entity/Resource to Row Item

The final step in configuring the search results is to create a mapping from the feature state to the row item used in the data table. This mapping is necessary to ensure that the correct data is displayed in the search results table.  
This is also the place to add translation keys for columns with the type `TRANSLATION_KEY`, if required.

### Template: Mapping from Entity to Row Item

| Directory | <root-of-ui-app>/src/app/<feature>/pages/<resource>-search |
| --------- | ---------------------------------------------------------- |
| File      | <resource>-search.selectors.ts                             |

Adust Selector in `<resource>-search.selectors.ts` 

```typescript
export const selectResults = createSelector(
  <resource>SearchSelectors.selectResults,
  (results: <resource>[]): RowListGridData[] => {
    return results.map((item) => ({
      imagePath: '',
      ...item,
      // ACTION S7: Create a mapping of the items and their corresponding translation keys
    }));
  }
);
```

---

### Example: Mapping Book Types

| Directory | bookstore/src/app/book/pages/book-search |
| --------- | ---------------------------------------- |
| File      | book-search.selectors.ts                 |

Example: Book Search Result Mapping 

```javascript
export const selectResults = createSelector(bookSearchSelectors.selectResults, (results: Book[]): RowListGridData[] => {
  return results.map((item) => ({
    imagePath: '',
    ...item,
    bookType: item.bookType
      ? `BOOK_SEARCH.RESULTS.BOOK_TYPES.${item.bookType.toUpperCase()}`
      : ''
    // ACTION S7: Create a mapping of the items and their corresponding translation keys
  }))
})
```

This example shows how to map a property `bookType` to a translation key.

## [](#action-s8)ACTION S8

Add translations for search result data

Ensure that all column headers and the mapped values in columns have the necessary translations added.

### Template: Translations for Search Results

| Directory | <root-of-ui-app>/src/app/assets/i18n |
| --------- | ------------------------------------ |
| Files     | en.json / de.json                    |

---

### Example: Translations for Book Search Results

| Directory | bookstore/src/app/assets/i18n |
| --------- | ----------------------------- |
| Files     | en.json / de.json             |

Adjust translations in `en.json` 

```json
  "BOOK_SEARCH": {
    ...
    "RESULTS": {
      "OUTPUT_FIELDS": "ACTION S8: Adjust translation keys for result columns",
      "BOOK_TITLE": "Book Title",
      "BOOK_TYPE": "Book Type",
      "BOOK_TYPES": {
        "CRIME": "Crime",
        "DRAMA": "Drama",
        "FANTASY": "Fantasy",
        "PROSE": "Prose",
        "SCIENCE": "Science"
      }
    },
    ...
```

Refer to the [Multi-Language Guide](../../../docs-guides-ui/angular/translation/multi-language.html) for more information.

Adjust translations in `de.json` 

```json
  "BOOK_SEARCH": {
    ...
    "RESULTS": {
      "OUTPUT_FIELDS": "ACTION S8: Adjust translation keys for result columns",
      "BOOK_TITLE": "Buchtitel",
      "BOOK_TYPE": "Buchtyp",
      "BOOK_TYPES": {
        "CRIME": "Krimi",
        "DRAMA": "Drama",
        "FANTASY": "Fantasie",
        "PROSE": "Prosa",
        "SCIENCE": "Wissenschaft"
      }
    },
  ...
```
