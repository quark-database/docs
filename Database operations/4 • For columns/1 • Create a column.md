#### Create a column

🔧 `create column in` - creates a column.

##### Parameters

* 📦 `name` of type `str` - the name of a table;
* 📦 `column` of type `column` - the column to add to the table;
* 📦 `fill? (default = "none")` of type `str` - the column to add to the table;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The column has been created.
```

##### Reports

1. The table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to create a column in a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the table name;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find what table you want to create a column in;
    3.  Rerun `create column in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. The column already exists
```
❌  An error occurred in Quark.

The context:  You tried to create a column in a table;
The error:    The column $name$ already exists;
What to do:   Please, find another name for a new column;

Try following these steps:
    1.  Run `list columns in`;
    2.  Come up with a name which is not in the list;
    3.  Rerun `create column in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

3. The lambda type is incorrect.
```
❌  An error occurred in Quark.

The context:  You tried to create a column in a table;
The error:    The column $name$ cannot contain $value$ returned by the lambda;
What to do:   See why your lambda could return a $type$;

Try following these steps:
    1.  Look at the lambda '$lambda$';
    2.  Try to run it with 'evaluate' instruction and paste values manually;
    3.  Rewrite the lambda and rerun `create column in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.