## Basic functions

Function | Brief Description
-------- | -----------------
[lookup](#lookup) | Import a set of values from a reference table.
[dedup](#dedup) | Remove duplicate records from the uploaded data.
[select](#select--reject) | Select (query) data from the Input based on a set of criteria.
[reject](#reject--reject) | Reject data from the Input based on a set of criteria.
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
column | The name of the column from the Input.
eval | Any one of the following criteria names: <ul><li>is</li><li>starts_with</li><li>ends_with</li><li>contains</li><li>is_less_than</li><li>is_greater_than</li><li>matches</li><li>is_type</li><li>is_blank</li><li>is_present</li><li>has_lookup</li></ul>
value | The term you are searching for. If the `value` key contains an array, it is assumed that you are searching for any of the values contained in the array.</li></ul>

Eval Criteria:

Eval | Description
---- | -----------
is | The value in `column` and the value in `value` match exactly.
is_not | The value in `column` and the value in `value` do not match.
starts_with | The input value starts with the same characters in `value`.
ends_with | The input value ends with the same characters in `value`.
contains | The input value contains the same characters in `value`.
is_less_than | The input value is less than the value in `value`.
is_greater_than | The input value is greater than the value in `value`.
matches | The input value matches a "regular expression" pattern defined in `value`. Use [Rubular](http://rubular.com/) to help you build a regular expression.
is_type | The input value is a known data type specified in `value`. Possible values include `Number`, `Date`, `String`, `Name`, `SSN`, and `Boolean`
is_blank | The input value is blank. The `value` parameter is ignored.
is_present | The input value is not blank. The `value` parameter is ignored.
has_lookup | (Under development)

### convert

Key name | Expected value
-------- | --------------
column | The name of the Input column to convert.
formula | A Convert formula object. A list of available conversion functions and their formats is listed, below.
evaluate | An Evaluation object, using the same structure as a select or reject. This makes it possible to apply `convert` based on criteria defined here.

Conversion Functions:

Key name | Description | Expected value
-------- | ----------- | --------------
concat | Concatenation - The expected value is an array with strings. Any string that is surrounded by double asterisks will be handled as a field lookup. | ["value 1", "value 2", "value 3"]<br>["value 1", "\*\*field_1\*\*"]
add | Addition - The expected value is an array with numbers or strings. Any string that is surrounded by double asterisks will be handled as a field lookup. | [1, 2, 3]<br>[\*\*base_salary\*\*, 100]
subtract | Subtraction - Same format as Addition. | 
multiply | Multiplication - Same format as Addition. | 