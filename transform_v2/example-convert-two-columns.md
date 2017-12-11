If the value in the `leave_term` column is greater than the value in the `end_date` column, the `work_status` will change to "A" and the `leave_term` colum will be blanked out.

To accomplish this:

Change the value in the `work_status` column to "A" if the value in the `leave_term` column is greater than the value in the `end_date` column.

Then, change the value in the `leave_term` column to blank if the value in the `work_status` column is "A".

```json
{
  "version": 2,
  "perform": [
    {
      "convert": {
        "column": "work_status",
        "formula": {
          "string": "A"
        },
        "condition": {
          "column": "leave_term",
          "eval": "is_greater_than",
          "value": "**end_date**"
        }
      }
    },
    {
      "convert": {
        "column": "leave_term",
        "formula": {
          "string": ""
        },
        "condition": {
          "column": "work_status",
          "eval": "is",
          "value": "A"
        }
      }
    }
  ],
  "save_output": "true"
}
```



