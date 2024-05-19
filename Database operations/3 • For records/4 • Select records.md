#### Select records

🔧 `select from` - selects the records from a table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;
* 📦 `if? (default = yes)` of type `str` - the lambda, the selection condition;
* 📦 `skip? (default = 0)` of type `int` - how many records meeting the condition have to be skipped;
* 📦 `limit? (default = max long)` of type `int` - the maximum record count can be selected;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The records have been selected.
```

##### Reports

1. The table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to select records from a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the table name;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find what table you want to select from;
    3.  Rerun `select from`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. The conditional lambda type is not boolean.
```
❌  An error occurred in Quark.

The context:  You tried to select records from a table;
The error:    The conditional lambda $if$ returned $value$, not a boolean;
What to do:   See why your lambda could return a $type$;

Try following these steps:
    1.  Look at the lambda '$if$';
    2.  Try to run it with 'evaluate' instruction and paste values manually;
    3.  Rewrite the condition and rerun `select from`;
```

3. The skip is negative.
```
❌  An error occurred in Quark.

The context:  You tried to select records from a table;
The error:    The skip cannot be negative (= $skip$);
What to do:   Remove the skip value or set it to whatever value you want;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

4. The limit is negative.
```
❌  An error occurred in Quark.

The context:  You tried to select records from a table;
The error:    The limit cannot be negative (= $limit$);
What to do:   Remove the limit value or set it to whatever value you want;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```


##### Result

| ...columns of the table | ...  |
| :---------------------: | :--- |
| ...the records selected | ...  |

<!-- or...
🚫 This instruction returns no result.
-->