#### Rename a column

🔧 `rename column in` - renames a column.

##### Parameters

* 📦 `name` of type `str` - the name of a table;
* 📦 `rename` of type `str` - the name of a column;
* 📦 `to` of type `str` - the new name of the column;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The column has been renamed
```

##### Reports

1. The table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to rename a column in a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the table name;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find what table you want to delete from;
    3.  Rerun `rename column in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

3. The column does not exist
```
❌  An error occurred in Quark.

The context:  You tried to rename a column in a table;
The error:    The column $name$ does not exist;
What to do:   Please, ensure that you did not misspell its name;

Try following these steps:
    1.  Run `list columns in`;
    2.  Find the column you want to rename;
    3.  Rerun `rename column in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

3. The column already exists
```
❌  An error occurred in Quark.

The context:  You tried to rename a column in a table;
The error:    The column $name$ already exists;
What to do:   Please, find another name for a new column;

Try following these steps:
    1.  Run `list columns in`;
    2.  Come up with a name which is not in the list;
    3.  Rerun `rename column in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.
