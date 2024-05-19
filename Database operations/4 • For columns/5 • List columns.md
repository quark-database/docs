#### List columns

🔧 `list columns in` - lists all the columns in the table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The columns have been listed.
```

##### Reports

1. The table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to list the columns in a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the table name;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find the table which columns you want to see;
    3.  Rerun `list columns in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

| `name` of type `str` |
| :------------------: |
| The list of columns  |

<!-- or...
🚫 This instruction returns no result.
-->