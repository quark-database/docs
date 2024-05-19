#### Get a variable value

🔧 `set variable value in` - gets the variable value in a table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;
* 📦 `called` of type `str` - the name of a variable;
* 📦 `to` of type `any` - a new value of the variable;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The variable value has been set.
```

##### Reports

1. The table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to set the variable value in a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the table name;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find what table you want to set a variable in;
    3.  Rerun `set variable value in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

1. The variable does not exist
```
❌  An error occurred in Quark.

The context:  You tried to set the variable value in a table;
The error:    The variable $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the variable name;

Try following these steps:
    1.  Run `list variables in`;
    2.  Find the variable you want to set the value of;
    3.  Rerun `set variable value in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.