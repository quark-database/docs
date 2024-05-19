#### Clear a table

🔧 `clear table` - clears a table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The table has been cleared, and now there are no records inside.
```

##### Reports

1. Table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to clear a table;
The error:    The table $name$ does not exist;
What to do:   Ensure that you did not misspell the name of the database;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find a table you want to clear;
    3.  Rerun `clear table`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.