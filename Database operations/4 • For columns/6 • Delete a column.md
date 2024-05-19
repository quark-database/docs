#### Delete a column

🔧 `delete column in` - deletes a column in a table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;
* 📦 `column` of type `str` - the name of a column;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The column is deleted.
```

##### Reports

1. The table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to delete a columns in a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the table name;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find the table in which you want to delete a column;
    3.  Rerun `delete column in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. The column does not exist
```
❌  An error occurred in Quark.

The context:  You tried to delete a columns in a table;
The error:    The column $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the column name;

Try following these steps:
    1.  Run `list columns in`;
    2.  Find what column you want to delete;
    3.  Rerun `delete column in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```


##### Result

🚫 This instruction returns no result.