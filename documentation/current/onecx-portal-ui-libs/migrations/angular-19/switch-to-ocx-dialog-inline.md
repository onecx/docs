# Replace ButtonDialogComponent

In OneCX v6, replace `ButtonDialogComponent` with `DialogInlineComponent` for inline dialogs with configurable buttons and dynamic content.

## [](#%5Fcode%5Fchanges)Code Changes

* Remove `ButtonDialogComponent` from `@onecx/portal-integration-angular`.
* Add `DialogInlineComponent` from `@onecx/angular-accelerator`.
* Replace tag `<ocx-button-dialog>` with `<ocx-dialog-inline>`.
* Migrate input properties and output events as per the mapping table below.

### [](#%5Fexample)Example

Before

```html
<ocx-button-dialog
  [config]="dialogConfig"
  (resultEmitter)="onDialogResult($event)">
  <p>Dialog Content to display</p>
</ocx-button-dialog>
```

```typescript
export class ExampleComponent {
  dialogConfig = {
    primaryButtonDetails: { key: 'OCX_BUTTON_DIALOG.CONFIRM' },
    secondaryButtonIncluded: true,
    secondaryButtonDetails: { key: 'OCX_BUTTON_DIALOG.CANCEL' },
    customButtons: [{ id: 'help', label: 'Help', alignment: 'left' }],
    autoFocusButton: 'primary'
  }

  onDialogResult(result: any) {
    console.log('Dialog result (inline):', result);
  }
}
```

After

```html
<ocx-dialog-inline
  [config]="dialogConfig"
  (resultEmitter)="onDialogResult($event)">
  <p>Dialog Content to display</p>
</ocx-dialog-inline>
```

```typescript
export class ExampleComponent {
  dialogConfig = {
    primaryButtonDetails: { key: 'OCX_BUTTON_DIALOG.CONFIRM' },
    secondaryButtonIncluded: true,
    secondaryButtonDetails: { key: 'OCX_BUTTON_DIALOG.CANCEL' },
    customButtons: [{ id: 'help', label: 'Help', alignment: 'left' }],
    autoFocusButton: 'primary'
  }

  onDialogResult(result: any) {
    console.log('Dialog result (inline):', result);
  }
}
```

## [](#%5Fproperties%5Fmapping)Properties Mapping

__Table 1\. Input Properties__
| ButtonDialogComponent | DialogInlineComponent | Notes                                                                                                                 |
| --------------------- | --------------------- | --------------------------------------------------------------------------------------------------------------------- |
| config                | config                | ButtonDialogConfig. Indicates the dialog configuration object for buttons, labels etc. No change in config structure. |

__Table 2\. Output Events__
| ButtonDialogComponent | DialogInlineComponent | Notes                                                               |
| --------------------- | --------------------- | ------------------------------------------------------------------- |
| resultEmitter         | resultEmitter         | Emits the type of button clicked (e.g. primary, secondary, custom). |
