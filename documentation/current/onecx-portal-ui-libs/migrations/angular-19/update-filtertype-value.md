# Update FilterType Value

In OneCX v6, two `FilterType` enum values were renamed.

## [](#%5Fupdate%5Fvalues)Update values

* `FilterType.EQUAL` → `FilterType.EQUALS`
* `FilterType.TRUTHY` → `FilterType.IS_NOT_EMPTY`

### [](#%5Fexample)Example

Before

```typescript
columns: [
  {
    id: 'amount',
    columnType: ColumnType.NUMBER,
    nameKey: 'FEATURE_SEARCH.RESULTS.AMOUNT',
    filterable: true,
    filterType: FilterType.EQUAL,
  }
  {
    id: 'available',
    columnType: ColumnType.STRING,
    nameKey: 'FEATURE_SEARCH.RESULTS.AVAILABLE',
    filterable: true,
    filterType: FilterType.TRUTHY,
  },
]
```

After

```typescript
columns: [
  {
    id: 'amount',
    columnType: ColumnType.NUMBER,
    nameKey: 'FEATURE_SEARCH.RESULTS.AMOUNT',
    filterable: true,
    filterType: FilterType.EQUALS,
  }
  {
    id: 'available',
    columnType: ColumnType.STRING,
    nameKey: 'FEATURE_SEARCH.RESULTS.AVAILABLE',
    filterable: true,
    filterType: FilterType.IS_NOT_EMPTY,
  },
]
```
