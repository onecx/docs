# OneCX GroupByCountDiagram

## [](#overview)Overview

This document aims to showcase how to manage GroupByCountDiagram component.

This component displays the search result data as a diagram. Please, visit the storybook page for the [GroupByCountDiagram component](https://main--65f7f64d4506c9f2dfe59383.chromatic.com/?path=/docs/components-groupbycountdiagramcomponent--docs) and interact with the examples to find out if the component is suitable for the desired use-case.

## [](#customization)Customization

The GroupByCountDiagram component allows for content customization:

* render different types of diagrams
* enable switching between diagram types
* set custom colors

To find out how to work with the GroupByCountDiagram component, please visit the [storybook page](https://main--65f7f64d4506c9f2dfe59383.chromatic.com/?path=/docs/components-groupbycountdiagramcomponent--docs) and interact with the examples to find out the required features. For more in-depth information on the GroupByCountDiagram component interface, please read the further documentation.

## [](#inputs)Inputs

__Table 1\. GroupByCountDiagram inputs__
| Property name         | Type                             | Default                     | Description                                                                                                                                                                                                                                                          |
| --------------------- | -------------------------------- | --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| sumKey                | string                           | FEATURE\_SEARCH.DIAGRAM.SUM | Translation key for label below the chart.                                                                                                                                                                                                                           |
| diagramType           | [DiagramType](#diagram-type)     | DiagramType.PIE             | Type of the chart to be displayed as.                                                                                                                                                                                                                                |
| supportedDiagramTypes | [DiagramType\[\]](#diagram-type) | \[\]                        | Add multiple Diagram types to be able to switch between them.                                                                                                                                                                                                        |
| data                  | unknown\[\]                      | \-                          | Data to be displayed as a diagram.                                                                                                                                                                                                                                   |
| columnType            | [ColumnType](#column-type)       | ColumnType.STRING           | Defines the type of the column.                                                                                                                                                                                                                                      |
| columnField           | string                           | ''                          | Defines which column data field to be displayed.                                                                                                                                                                                                                     |
| column                | [DiagramColumn](#diagram-column) | \-                          | Defines which columns and its type to be displayed.                                                                                                                                                                                                                  |
| fillMissingColors     | boolean                          | true                        | Determines if diagram should generate the colors for the data that does not have any set. Set to false will result in using the provided colors only if every data item has one. When at least one item does not have a color set, diagram will generate all colors. |
| colors                | Record<string, string>           | {}                          | Defines custom color for data items.                                                                                                                                                                                                                                 |

## [](#outputs)Outputs

__Table 2\. GroupByCountDiagram outputs__
| Property name         | Type                                                                                        | Description                                                                                                    |
| --------------------- | ------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| dataSelected          | EventEmitter<any>                                                                           | Emits data object upon clicking a diagram element.                                                             |
| diagramTypeChanged    | EventEmitter<[DiagramType](#diagram-type)\>                                                 | Emits the [DiagramType](#diagram-type) when one of the supported diagram types is selected to switch the type. |
| componentStateChanged | EventEmitter<[GroupByCountDiagramComponentState](#group-by-count-diagram-component-state)\> | Emits the selected [DiagramType](#diagram-type) to ensure consistent component state.                          |

## [](#types)Types

### [](#diagram-type)DiagramType

DiagramType enum

```javascript
    export const enum DiagramType {
        PIE = 'PIE',
        VERTICAL_BAR = 'VERTICAL_BAR',
        HORIZONTAL_BAR = 'HORIZONTAL_BAR',
    }
```

### [](#column-type)ColumnType

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

### [](#diagram-column)DiagramColumn

DiagramColumn type

```javascript
    export type DiagramColumn = { columnType: ColumnType; id: string }
```

### [](#group-by-count-diagram-component-state)GroupByCountDiagramComponentState

GroupByCountDiagramComponentState interface

```javascript
    export interface GroupByCountDiagramComponentState {
        activeDiagramType?: DiagramType
    }
```
