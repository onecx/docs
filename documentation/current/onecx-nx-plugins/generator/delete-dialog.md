# undefined

### [](#%5Fcreate%5Fdelete%5Fdialog)Create Delete Dialog

The fastest way to create a delete dialog in a feature module is to use the OneCX generator.

To run the generator, execute the following command:

nx generate <namespaceOfTheGenerator>/angular-generator:delete <feature>

* _<feature>_: see [here](glossary.html#feature).

| |  Next, the CLI will ask you whether you want to customize names for the generation. When answering yes, the next few questions will ask you about names for the API. This can be useful if you want to adapt to a legacy API. When modifying names, assure that you use the same custom names for all generated components of the feature (search, details, create-update, delete) for the data object name, and the api service name as these ones are shared. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
