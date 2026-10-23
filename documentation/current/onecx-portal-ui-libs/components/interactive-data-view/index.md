# OneCX InteractiveDataView

## [](#overview)Overview

This document aims to showcase how to manage InteractiveDataView Component.

## [](#inputs)Column group selector dialog inputs

The `InteractiveDataView` hosts a column group selector dialog (shown in the `table` layout). These inputs configure that dialog and are forwarded to the hosted `CustomGroupColumnSelectorComponent`.

__Table 1\. Column group selector dialog inputs__
| Input name                         | Type    | Default | Description                                                                                                                                                                                                                                       |
| ---------------------------------- | ------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| draggableColumnGroupSelectorDialog | boolean | true    | Whether the column selection dialog can be dragged by the user.                                                                                                                                                                                   |
| resizableColumnGroupSelectorDialog | boolean | true    | Whether the column selection dialog can be resized by the user. Independent of draggableColumnGroupSelectorDialog.                                                                                                                                |
| restoreColumnGroupSelectorOrder    | boolean | false   | When enabled, transferring columns rebuilds the active and inactive lists in the order of the configured columns, so the active columns keep the main column order after a save. When disabled, the normal pick-list transfer order is preserved. |

## [](#related-interfaces)Related Interfaces

* [DataTableColumn](data-table-column.html)
