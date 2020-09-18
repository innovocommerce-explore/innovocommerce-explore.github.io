---
id: version-1.2.2-rules
title: Rules
original_id: rules
---

The document analysis modeling support the inclusion of validation rules.

A validation rule is a combination of three components:
* Validated field: This is the name of the model field against which the validation will indicate if the rule was satisified or not.
* Rule expression: An expression that will be evaluated per document to determine if the rule is satisified.
* Error description expression: An expression that will be evaluated to display a text when the rule has **not** been satisfied.

## Validated field

The validation field name corresponds to the field as defined in the document analysis model. See [Document Analysis Models](doc2.md)

For example: `field_name`, `version`.

## Rule expression

This expression is the heart of the rule as it defines how the validation will occur. It is a logical expression that indicates how a field should be evaluated.

The rule expressions can have *field names*, *values*, *comparisons*, *logical operations*:
* Field names: these are the same fields as defined in the document analysis models. For example, `version`.
* Values: These indicate numbers, strings, or dates. To represent a string it must be enclosed by either `"` or `'`. All dates must be represented in a string, and should be in a format that can be used to compare it with the date format of the defined document analysis model. For example, a number: `3.25`; both `"InnovoCommerce Xenon"` and `'InnovoCommerce Xenon'` represent the same string, but not `'"InnovoCommerce Xenon"'` as the latter is including the `"` character as part of the string (the single quote is defining the begininng and end of the string); a valid date is `"2020-09-01"`.
* Comparisons: In order to express how a field is related to another field or to a given value comparisons are needed. For example, do you want to check if the `version` field is *equal* to a *numeric value* then you would use an *equality comparison.* 
* Logical operations: If you want to combine multiple comparisons logical operations are helpful. For example, do you want to check if `version` field must be equal to a given value *and* `doc_name` must equal to a known string? This can be accomplished by joining both comparison by the **AND** logical operation.

### Comparisons

Supported comparisons:

* Equality: Represented by `=`. For example, field `persons` must equal 3: `persons = 3`
* Inequality: Represented by `<>`. For example, field `patient_name` must not equal **John Smith**: `patient_name <> 'John Smith'`
* Less than or before a certain date: Represented by `<`. For example, field `num_persons` must be less than 10 `num_persons < 10`.
* Less than or equal to or before or on a certain date. Represented by `<=`. For example, field `signature_date` must be before or on September 1st, 2020: `signature_date <= '2020-09-01'`
* More than or after a certain date: Represented by `>`.
* More than or equal to or after or on a certain date: Represented by `>=`.

### Logical Operations

These operations logically join comparisons or modify its behavior.


### Examples

* `version` field must equal **2**: `version = 2`
* `version` field must be more than **2**: `version > 2`
* `version_date` field must be later than or equal to **September 1, 2020**: `version_date >= '2020-09-01'`
* `version` field must be equal to **2** *and* `version_date` field must be later than or equal to **September 1, 2020**: `version_date = 2 and version_date >= '2020-09-01'`
* `doc_name` field must *not* equal **Consent Form**: `doc_name <> "Consent Form"`
* `doc_name` field must be equal to the field `doc_title`: `doc_name = doc_title`

## Error Description Expression





