# DataTableColumn

## [](#data-table-column-properties-overview)DataTableColumn properties overview

__Table 1\. DataTableColumn interface__
| Property name        | Type       | Description                                                                                                                                                                                                                                                                                                           |
| -------------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| columnType           | ColumnType | Defines the type of the column.                                                                                                                                                                                                                                                                                       |
| id                   | string     | The id of the column.                                                                                                                                                                                                                                                                                                 |
| nameKey              | string     | Translation key for the column header name.                                                                                                                                                                                                                                                                           |
| tooltipKey?          | string     | Translation key for the column header tooltip. Used when tooltip is omitted or empty. If both properties are omitted or empty, no tooltip is shown. Only applies to the table layout. Use for supplementary information only, the tooltip is not keyboard accessible.                                                 |
| tooltip?             | string     | Plain text for the column header tooltip, without translation. A non-empty value takes precedence over tooltipKey. Only applies to the table layout. Use for supplementary information only, the tooltip is not keyboard accessible.                                                                                  |
| sortable?            | boolean    | Indicates if the column is sortable.                                                                                                                                                                                                                                                                                  |
| filterable?          | boolean    | Indicates if the column is filterable.                                                                                                                                                                                                                                                                                |
| filterType?          | FilterType | Defines which type of filter is used.                                                                                                                                                                                                                                                                                 |
| predefinedGroupKeys? | string\[\] | Defines the group set in which the following column is available. Additionally, the predefinedGroups can be selected from a dropdown menu at the top of the search results table. If you want your search column to belong only to the default column group, then only add FEATURE\_SEARCH.PREDEFINED\_GROUP.DEFAULT. |
| dateFormat?          | string     | Allows customization of the date format. Uses Angular DatePipe format.                                                                                                                                                                                                                                                |

ColumnType enum

```javascript
    export const enum ColumnType {
        STRING = 'STRING',
        NUMBER = 'NUMBER',
        DATE = 'DATE',
        RELATIVE_DATE = 'RELATIVE_DATE',
        TRANSLATION_KEY = 'TRANSLATION_KEY',
    }
```

FilterType enum

```javascript
  export declare enum FilterType {
      EQUAL = "EQUAL",
      TRUTHY = "TRUTHY"
  }
```

| Type   | Description                                                              |
| ------ | ------------------------------------------------------------------------ |
| EQUAL  | Will create a set of unique values for filtering.                        |
| TRUTHY | Will always have two filter options which result in empty and not empty. |
