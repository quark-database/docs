#### Delete a table

🔧 `delete table` - deletes a table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The table has been deleted.
```

##### Reports

1. The table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to delete a table;
The error:    The table $name$ does not exist;
What to do:   Ensure that you did not misspell the name of the table;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find the table you want to delete;
    3.  Rerun `delete table`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.