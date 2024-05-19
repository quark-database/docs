#### Count records

🔧 `count records in` - counts records in a table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The records have been counted.
```

##### Reports

1. Table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to count records in a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you did not misspell it;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find a table you want to count records in;
    3.  Rerun `count records in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

|     `count` of type `int`     |
| :---------------------------: |
| The record count in the table |

<!-- or...
🚫 This instruction returns no result.
-->