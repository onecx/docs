# Configure Search Results

The generated React search page displays results in an interactive data view (a sortable table).  
The columns shown in the table are defined by the `<resource>SearchColumns` array in the `<resource>-search.types.ts` file and consumed by the results section component.

Steps to add Search Results columns

1. Add or adjust the column definitions in `<resource>-search.types.ts`.
2. The results section component renders these columns automatically; adjust it only for custom cell rendering.
3. Add the matching translation keys for the column headers (see [Search Add-ons](search-add-ons.html)).

## [](#action-s5)ACTION S5

If not yet done, specify the base entity properties of your `<Resource>` schema in the OpenAPI specification. The generated schema marks the place with `ACTION E: Add entity properties`, see [Map the API and Prepare Mock Data](mock-api.html).

## [](#action-s6)ACTION S6

Define Search Results columns (types)

Each column has a `field` (a key of the result row) and a `headerKey` (an i18n key for the column header). The generated template ships with a single `id` column.

### Template: Generated columns

| Directory | src/pages/<feature>/<resource>-search |
| --------- | ------------------------------------- |
| File      | <resource>-search.types.ts            |

ACTION S6 in `<resource>-search.types.ts` 

```typescript
// Row shape shown in the results table (aligned to the generated <Resource> model)
export type <Resource>SearchRow = <Resource>;

export interface SearchColumn<T extends object> {
  field: keyof T;
  headerKey: string;
}

// ACTION S6: Define search results columns
export const <resource>SearchColumns: SearchColumn<<Resource>SearchRow>[] = [
  {
    field: 'id',
    headerKey: '<RESOURCE>_SEARCH.RESULTS.ID',
  },
  // ACTION S6: add more columns to match your entity
];
```

Add one entry per column you want to display in the results table.

---

### Example: Book result columns

| Directory | bookstore/src/pages/book/book-search |
| --------- | ------------------------------------ |
| File      | book-search.types.ts                 |

Example: Adjustments in `book-search.types.ts` 

```typescript
export const bookSearchColumns: SearchColumn<BookSearchRow>[] = [
  {
    field: 'id',
    headerKey: 'BOOK_SEARCH.RESULTS.ID',
  },
  {
    field: 'bookTitle',
    headerKey: 'BOOK_SEARCH.RESULTS.BOOK_TITLE',
  },
  {
    field: 'bookAuthor',
    headerKey: 'BOOK_SEARCH.RESULTS.BOOK_AUTHOR',
  },
];
```

Where **bookTitle** and **bookAuthor** are properties of the generated `Book` model.

## [](#action-s6-component)ACTION S6 (results section)

The results section component reads the columns from `<resource>SearchColumns` and renders them via the shared `InteractiveDataView`. In most cases no change is needed here, but the `ACTION S6` marker shows where to adjust the column mapping (e.g. custom cell content).

### Template: Generated results columns mapping

| Directory | src/components/<feature>                        |
| --------- | ----------------------------------------------- |
| File      | <resource>-search-results-section.component.tsx |

ACTION S6 in `<resource>-search-results-section.component.tsx` 

```tsx
    /* ACTION S6: Define/adjust result columns */
    columns={<resource>SearchColumns.map((column) => ({
      field: column.field,
      header: t(column.headerKey),
      sortable: true,
    }))}
```

Adjust the mapping if you need non-sortable columns or custom rendering.

| |  Each column header references a translation key under <RESOURCE>\_SEARCH.RESULTS. Remember to add those keys, see [Search Add-ons](search-add-ons.html). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
