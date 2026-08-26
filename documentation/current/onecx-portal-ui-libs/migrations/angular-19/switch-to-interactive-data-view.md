# Replace DataViewControlsComponent

In OneCX v6, the InteractiveDataViewComponent replaces the following use cases:

* Replace **p-dataView** and **DataViewControlsComponent** template with **InteractiveDataViewComponent**
* Replace **p-table** and **DataViewControlsComponent** template with **InteractiveDataViewComponent**.

## [](#%5Fcode%5Fchanges)Code Changes

* Remove `<ocx-data-view-controls>` and `DataViewControlsComponent` from `@onecx/portal-integration-angular`
* Add `InteractiveDataViewComponent` from `@onecx/angular-accelerator`.
* Replace the entire `<p-dataView>` or `<p-table>` with `<ocx-interactive-data-view>`
* Remove `DataViewModule` from `primeng/dataview` if not used elsewhere
* Add `<ocx-interactive-data-view>` and update input properties and output events as per tables below

### [](#%5Fexamples)Examples

**Example: p-dataView & DataViewControlsComponent to InteractiveDataViewComponent**.Before

```html
<p-dataView [value]="items" [layout]="'grid'" [paginator]="true" [rows]="20">
  <ng-template pTemplate="header">
    <ocx-data-view-controls
      [supportedViews]="['grid']"
      [initialViewMode]="'grid'"
      [filterValue]="filterValue"
      [enableFiltering]="true"
      (filterChange)="onFilterChange($event, dataView)"
      [enableSorting]="false"
    ></ocx-data-view-controls>
  </ng-template>

  <ng-template pTemplate="gridItem" let-item>
    <div class="card">
      <div>{{ item.name }}</div>
    </div>
  </ng-template>
</p-dataView>
```

After

```html
<ocx-interactive-data-view
  [data]="items"
  [supportedViewLayouts]="['grid']"
  [layout]="'grid'"
  [columns]="columns"
  [filters]="filters"
  [filter]="filterValue"
  [clientSideFiltering]="true"
  [emptyResultsMessage]="'ACTIONS.SEARCH.NO_DATA' | translate"
  (filtered)="onFilterChange($event)"
  (sorted)="onSortChange($event)"
  (dataViewLayoutChange)="onDataViewChange($event)"
>
  <ng-template pTemplate="item" let-item>
    <div class="card">
      <div>{{ item.name }}</div>
    </div>
  </ng-template>
</ocx-interactive-data-view>
```

**Example: p-table & DataViewControlsComponent to InteractiveDataViewComponent**

Before

```html
<p-table [value]="items" [paginator]="true" [rows]="20">
  <ng-template pTemplate="header">
    <ocx-data-view-controls
      [supportedViews]="['table']"
      [initialViewMode]="'table'"
      [filterValue]="filterValue"
      [enableFiltering]="true"
      (filterChange)="onFilterChange($event, table)"
      [enableSorting]="true"
    ></ocx-data-view-controls>
  </ng-template>
  <ng-template pTemplate="body" let-item>
    <tr>
      <td>{{ item.name }}</td>
      <td>{{ item.value }}</td>
    </tr>
  </ng-template>
  <ng-template #emptymessage>
    <tr>
        <td colspan="5">{{'ACTIONS.SEARCH.NO_DATA' | translate}}</td>
    </tr>
  </ng-template>
</p-table>
```

After

```html
<ocx-interactive-data-view
  [data]="items"
  [supportedViewLayouts]="['table']"
  [layout]="'table'"
  [columns]="columns"
  [filters]="filters"
  [filter]="filterValue"
  [clientSideFiltering]="true"
  [clientSideSorting]="true"
  [emptyResultsMessage]="'ACTIONS.SEARCH.NO_DATA' | translate"
  (filtered)="onFilterChange($event)"
  (sorted)="onSortChange($event)"
  (dataViewLayoutChange)="onDataViewChange($event)"
>
  <ng-template pTemplate="item" let-item>
    <tr>
      <td>{{ item.name }}</td>
      <td>{{ item.value }}</td>
    </tr>
  </ng-template>
</ocx-interactive-data-view>
```

## [](#%5Fproperties%5Fmapping)Properties Mapping

Input Properties (DataViewControlsComponent) 

| DataViewControlsComponent | InteractiveDataViewComponent | Notes                                                                                                                                                                                                                                                                                              |
| ------------------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| supportedViews            | supportedViewLayouts         | Indicates available layouts. Example: \[supportedViewLayouts\]="\['list', 'grid', 'table'\]".                                                                                                                                                                                                      |
| initialViewMode           | layout                       | Sets initial layout. Example: \[layout\]="'list'".                                                                                                                                                                                                                                                 |
| filterValue               | filter                       | Filters to apply. Use the value key in each Filter object. Example: const filters: Filter\[\] = \[ { columnId: 'category', filterType: FilterType.EQUALS, value: \['books', 'electronics'\] } \]                                                                                                   |
| enableFiltering           | clientSideFiltering          | Enable client-side filtering. Example: \[clientSideFiltering\]="true"                                                                                                                                                                                                                              |
| enableSorting             | clientSideSorting            | Enable client-side sorting. Example: \[clientSideSorting\]="true"                                                                                                                                                                                                                                  |
| sortingOptions            | columns                      | Configure sorting per column by setting sortable on each DataTableColumn. Example: const columns: DataTableColumn\[\] = \[ { id: 'name', nameKey: 'OCX\_DATA\_TABLE.COLUMN.NAME', columnType: ColumnType.STRING, sortable: true } \];                                                              |
| defaultSortOption         | sortField                    | Use the column id for the default sort field. Example: \[sortField\]="'name'"                                                                                                                                                                                                                      |
| defaultSortDirection      | sortDirection                | Use the DataSortDirection enum to specify the sort direction. Example: \[sortDirection\]=DataSortDirection.ASCENDING                                                                                                                                                                               |
| columnDefinitions         | columns                      | Use id (instead of field) and nameKey for translated column names. Control visible columns with displayedColumnKeys. Example: const columns: DataTableColumn\[\] = \[ { id: 'name', nameKey: 'OCX\_DATA\_TABLE.COLUMN.NAME', columnType: ColumnType.STRING } \]; displayedColumnKeys = \['name'\]; |
| columnTemplates           | pTemplate with selectors     | Use p-template with a selector. For more information, see the Template Transformation section.                                                                                                                                                                                                     |
| dropdownPlaceholderText   | \-                           | Deprecated. Use translations (i18n); there is no direct input in the new component.                                                                                                                                                                                                                |
| filterColumns             | filters                      | Use filters with clientSideFiltering. In each filter object, provide columnId and filterType.                                                                                                                                                                                                      |
| translations              | \-                           | Use i18n / translation keys.                                                                                                                                                                                                                                                                       |

Input Properties (p-dataView) 

| p-dataView                | InteractiveDataViewComponent      | Notes                                                                                                                                                                    |
| ------------------------- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| value                     | data                              | Defines the component’s data source. Example: \[data\]="items"                                                                                                           |
| paginator                 | listGridPaginator, tablePaginator | listGridPaginator and tablePaginator are enabled by default                                                                                                              |
| rows                      | pageSize                          | Number of items per page. Example: \[pageSize\]="20".                                                                                                                    |
| rowsPerPageOptions        | pageSizes                         | Array of page size options. Example: \[pageSizes\]="\[20, 60, 100\]"                                                                                                     |
| alwaysShowPaginator       | \-                                | The paginator is shown listGridPaginator                                                                                                                                 |
| showCurrentPageReport     | \-                                | The paginator shows the current page report by default when enabled.                                                                                                     |
| currentPageReportTemplate | \-                                | Use the currentPageShowingKey translation key to render content. The currentPageReportTemplate is shown when pagination is enabled. Default: 'OCX\_DATA\_TABLE.SHOWING'. |
| filterBy                  | \-                                | Use clientSideFiltering and specify filterType in the Filter object.                                                                                                     |
| emptyMessage              | emptyResultsMessage               | Message displayed when no data is available.                                                                                                                             |

Input Properties (p-table) 

| p-table            | InteractiveDataViewComponent | Notes                                                                   |
| ------------------ | ---------------------------- | ----------------------------------------------------------------------- |
| value              | data                         | Data source for the table. \[data\]="items"                             |
| columns            | columns                      | Column definitions. Use id and nameKey for each column.                 |
| paginator          | tablePaginator               | Enable table pagination. \[tablePaginator\]="true" (enabled by default) |
| rows               | pageSize                     | Number of items per page. \[pageSize\]="20"                             |
| rowsPerPageOptions | pageSizes                    | Array of page size options. \[pageSizes\]="\[20, 60, 100\]"             |

Output Events 

| DataViewControlsComponent       | InteractiveDataViewComponent | Notes                                                            |
| ------------------------------- | ---------------------------- | ---------------------------------------------------------------- |
| sortChange, sortDirectionChange | sorted                       | Emits { sortColumn, sortDirection }                              |
| filterChange                    | filtered                     | Emits Filter\[\]                                                 |
| dataViewChange                  | dataViewLayoutChange         | Emits 'list', 'grid', or 'table'                                 |
| columnsChange                   | displayedColumnKeysChange    | Emits string\[\] which contains the ids of the displayed columns |

## [](#%5Fadditional%5Fnotes)Additional Notes

### [](#%5Ftemplate%5Ftransformation)Template Transformation

For p-dataView 

| p-dataView           | InteractiveDataViewComponent | Notes                                                                                       |
| -------------------- | ---------------------------- | ------------------------------------------------------------------------------------------- |
| pTemplate="header"   | pTemplate="topCenter"        | Keep header template for custom content. Remove only ocx-data-view-controls from inside it. |
| pTemplate="gridItem" | pTemplate="item"             | Use let-item let-i="index" same applies for listItem                                        |

Before:

```html
<ng-template let-roles pTemplate="gridItem">
  <section>
    <article *ngFor="let role of roles; index as i">
      <a (click)="onEditRole($event, role)" [id]="'ws_roles_grid_data_row_' + i"> ... </a>
    </article>
  </section>
</ng-template>
```

After:

```html
<ng-template pTemplate="item" let-item let-i="index">
  <section>
    <article class="col-...">
      <a (click)="onEditRole($event, item)" [id]="'ws_roles_grid_data_row_' + i"> ... </a>
    </article>
  </section>
</ng-template>
```

For p-table 

| p-table            | InteractiveDataViewComponent | Notes                                                                                       |
| ------------------ | ---------------------------- | ------------------------------------------------------------------------------------------- |
| pTemplate="header" | pTemplate="topCenter"        | Keep header template for custom content. Remove only ocx-data-view-controls from inside it. |
| pTemplate="body"   | pTemplate="item"             | Use let-item for row context in table layout                                                |

Before:

```html
<ng-template pTemplate="body" let-item>
  <tr>
    <td>{{ item.name }}</td>
    <td>{{ item.value }}</td>
  </tr>
</ng-template>
```

After:

```html
<ng-template pTemplate="item" let-item>
  <tr>
    <td>{{ item.name }}</td>
    <td>{{ item.value }}</td>
  </tr>
</ng-template>
```
