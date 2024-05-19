#### Swap columns

🔧 `swap columns in` - swaps two columns in a table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;
* 📦 `swap` of type `str` - the name of the first column;
* 📦 `with` of type `str` - the name of the second column;

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
    2.  Find the table you want to swap columns in;
    3.  Rerun `rename column in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. The column does not exist
```
❌  An error occurred in Quark.

The context:  You tried to rename a column in a table;
The error:    The column $name$ does not exist;
What to do:   Please, ensure that you did not misspell its name;

Try following these steps:
    1.  Run `list columns in`;
    2.  Find the columns you want to swap;
    3.  Rerun `rename column in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

3. The column names are the same
```
❌  An error occurred in Quark.

The context:  You tried to rename a column in a table;
The error:    These two names are identical;
What to do:   Please, replace one of these names with another column name;

Try following these steps:
    1.  Run `list columns in`;
    2.  Find the columns you want to swap;
    3.  Rerun `rename column in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.
