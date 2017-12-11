Change the value in the work_status column to "A" if the value in the leave_`term` column is greater than the value in the `enddate` column

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



