# Migration Guide for 1000kit Parameter Service

## [](#%5Foverview)Overview

The parameter service has been refactored to simplify the handling of parameters. Previously, parameters had a fixed, defined type, and included fields like "UNIT", "rangeFrom", and "rangeTo". The new service allows parameters to be either primitive types or JSON objects, giving applications the flexibility to interpret these objects as needed.

## [](#%5Fchanges)Changes

### [](#%5Fparameter%5Ftypes)Parameter Types

* **Old**: Parameters had a fixed, defined type.
* **New**: Parameters can be primitive types (e.g., string, number) or JSON objects.

### [](#%5Funits%5Fand%5Frange%5Ffields)Units and Range Fields

* **Old**: Parameters included "UNIT", "rangeFrom", and "rangeTo" fields.
* **New**: These fields have been removed. Applications can now include units and range information or any other field within the JSON object if needed.

## [](#%5Fmigration%5Fsteps)Migration Steps

### [](#%5Freview%5Fparameter%5Fdefinitions)Review Parameter Definitions

* Identify all parameters currently using the "UNIT", "rangeFrom", and "rangeTo" fields.
* Determine if these parameters can be converted to JSON objects.

### [](#%5Fupdate%5Fparameter%5Fhandling)Update Parameter Handling

* For parameters requiring units and range information, create a JSON object with fields for these values.
* Example:

{
  "value": 100,
  "units": "ms",
  "rangeFrom": 50,
  "rangeTo": 150
}

### [](#%5Fmodify%5Fapplication%5Flogic)Modify Application Logic

* Update application code to handle the new parameter format.
* Ensure applications correctly interpret JSON objects and extract necessary fields.

### [](#%5Ftesting)Testing

* Test the updated parameter handling to ensure compatibility and correctness.
* Validate that applications correctly interpret and use the new parameter format.

## [](#%5Fsummary)Summary

The refactored parameter service offers greater flexibility by allowing parameters to be primitive types or JSON objects. Applications now have the responsibility to interpret these objects, including handling units and range information within the JSON structure.
