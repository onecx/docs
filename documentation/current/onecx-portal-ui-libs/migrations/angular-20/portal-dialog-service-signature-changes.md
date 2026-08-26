# PortalDialogService Signature Changes

In version 7, updates in the PrimeNG Dynamic Dialog API (introduced in PrimeNG 20) required changes to the `PortalDialogService` method signatures.

## [](#%5Fsummary%5Fof%5Fchanges)Summary of Changes

* The return type of `openDialog<T>` changed from: `Observable<DialogState<T>>` to `Observable<DialogState<T> | null>`

## [](#%5Fupdate%5Fyour%5Fapplication)Update Your Application

* Adjust your handling of `openDialog()` results. Since the method may now return `Observable<null>`, your code must handle the case where a dialog cannot be created.

| |  If openDialog() returns Observable<null>, the dialog creation has failed. Check the browser console for PortalDialogService warnings or errors. |
| -------------------------------------------------------------------------------------------------------------------------------------------------- |
