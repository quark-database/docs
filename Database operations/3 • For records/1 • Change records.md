#### Change records

🔧 `change records in` - changes the records in a table with a lambda expression.

##### Parameters

* 📦 `name` of type `str` - the name of a table;
* 📦 `change` of type `str` - the name of a column to change values of;
* 📦 `by` of type `str` - the lambda which values will be used for each record;
* 📦 `if? (default = yes)` of type `str` - the lambda conditional for what records should be changed;

##### Success message

```
✅  The records has been changed.
```

##### Reports

1. The table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to change the records in a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the table name;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find what table you want to change records in;
    3.  Rerun `change records in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. The column does not exist
```
❌  An error occurred in Quark.

The context:  You tried to change the records in a table;
The error:    The column $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the column name;

Try following these steps:
    1.  Run `list columns in`;
    2.  Find what column you want to change values of;
    3.  Rerun `change records in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

3. The lambda type is incorrect.
```
❌  An error occurred in Quark.

The context:  You tried to change the records in a table;
The error:    The column $name$ cannot contain $value$ returned by the lambda;
What to do:   See why your lambda could return a $type$;

Try following these steps:
    1.  Look at the lambda '$lambda$';
    2.  Try to run it with 'evaluate' instruction and paste values manually;
    3.  Rewrite the lambda and rerun `change records in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

4. The lambda type is incorrect.
```
❌  An error occurred in Quark.

The context:  You tried to change the records in a table;
The error:    The column $name$ cannot contain $value$ returned by the lambda;
What to do:   See why your lambda could return a $type$;

Try following these steps:
    1.  Look at the lambda '$lambda$';
    2.  Try to run it with 'evaluate' instruction and paste values manually;
    3.  Rewrite the lambda and rerun `change records in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

4. The lambda type is incorrect.
```
❌  An error occurred in Quark.

The context:  You tried to change the records in a table;
The error:    The column $name$ cannot contain $value$ returned by the lambda;
What to do:   See why your lambda could return a $type$;

Try following these steps:
    1.  Look at the lambda '$lambda$';
    2.  Try to run it with 'evaluate' instruction and paste values manually;
    3.  Rewrite the lambda and rerun `change records in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

5. The conditional lambda type is not boolean.
```
❌  An error occurred in Quark.

The context:  You tried to change the records in a table;
The error:    The conditional lambda $if$ returned $value$, not a boolean;
What to do:   See why your lambda could return a $type$;

Try following these steps:
    1.  Look at the lambda '$if$';
    2.  Try to run it with 'evaluate' instruction and paste values manually;
    3.  Rewrite the condition and rerun `change records in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

> [!WARNING]
> Syntax errors from lambdas in `📦 by` must be handled outside the instruction code.

> [!WARNING]
> Errors related to column properties are listed in the properties documentation.

##### Result

🚫 This instruction returns no result.