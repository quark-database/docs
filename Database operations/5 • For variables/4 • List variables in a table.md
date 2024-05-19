#### List variables in a table

🔧 `list variables in` - lists all the variables in a table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The variables have been listed.
```

##### Reports

1. The table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to list the variables in a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the table name;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find of which table you want to see the variables;
    3.  Rerun `list variables in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

|    `name` of type `str`    | `value` of type `any` |
| :------------------------: | :-------------------: |
| The names of the variables |     Their values      |

<!-- or...
🚫 This instruction returns no result.
-->