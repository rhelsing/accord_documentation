## Basic functions

Function | Brief Description
-------- | -----------------
[lookup](#lookup) | Import a set of values from a reference table.
[dedup](#dedup) | Remove duplicate records from the uploaded data.
[select](#select) | Select (query) data from the Input based on a set of criteria.
[reject](#reject) | Reject data from the Input based on a set of criteria.
[convert](#convert) | Use a formula to change the data contained in a column.
[derive](#derive) | Create a new column in the Output and populate the column with values based on a formula.
[aggregate](#aggregate) | Turn the Output into an aggregate report.
[map](#map) | Define field mappings between Input and new columns generated through calculations, and Output.

## Function Parameters

### lookup

Key Name | Expected Value
-------- | --------------
input_key | The name of the key column in the input. Use an array if multiple columns need to be used as a key.
lookup_source | An object with `layout` or `file_drop` as the key name, and the name of the source as the value.
lookup_key | The name of the key column in the lookup source. Use an array if multiple columns need to be used as a key -- make sure the array contains the same number of fields as in the input_key, listed in the same order.

### dedup

Key Name | Expected Value
-------- | --------------
column | The name of the input column. Use an array to specify multiple columns.

### select & reject

Basic Evaluation:

Key Name | Expected Value
-------- | --------------
column | The name of the column from the Input. Columns generated through a `lookup` or `derive` **placeholder** describe how the alias name will be generated.
eval | Any one of the following criteria names: <ul><li>is</li><li>starts_with</li><li>ends_with</li><li>contains</li><li>is_less_than</li><li>is_greater_than</li><li>matches</li><li>is_type</li><li>is_blank</li><li>is_present</li><li>has_lookup</li><li>lookup</li></ul>
value | The term you are searching for. If the `value` key contains an array, it is assumed that you are searching for any of the values contained in the array.<br><br>Please note the following restrictions, based on the value for the `eval` key:<ul><li>A `matches` eval will expect a Regular Expression **placeholder link** as the `value`. You should use this option only if you know what you're doing.</li><li>A `is_type` eval expects a known data type as the `value`. Possible values include: "Number", "Date", "String", "Name", "SSN", and "Boolean".</li><li>A `is_blank` or `is_present` eval does not require a `value`.</li><li>A `has_lookup` eval can only be used if a `lookup` Key is present. The value should match the value supplied for the `input_key`.</li></ul>


