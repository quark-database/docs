#### Reorder columns

🔧 `reorder columns in` - changes the order of the columns in a table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;
* 📦 `order` of type `array of str` - the new order of columns;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The columns has been reordered.
```

##### Reports

1. The table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to reorder the columns in a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the table name;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find the table which columns you want to reorder;
    3.  Rerun `reorder columns in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. The column list does not match the table columns
```
❌  An error occurred in Quark.

The context:  You tried to reorder the columns in a table;
The error:    The columns do not match the table;
What to do:   Please, check the list of your columns and the table's;

Try following these steps:
    1.  Run `list columns in`;
    2.  Look at the list of your columns;
    3.  Rerun `reorder columns in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.