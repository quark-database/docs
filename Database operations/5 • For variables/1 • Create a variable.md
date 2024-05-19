#### Create a variable

🔧 `create variable in` - creates a variable in a table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;
* 📦 `called` of type `str` - the name of a variable;
* 📦 `with value` of type `any` - the value of a variable;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The variable is created.
```

##### Reports

1. The table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to create a variable in a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you didn't misspell the table name;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find what table you want to create a variable in;
    3.  Rerun `create variable in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. The variable already exists
```
❌  An error occurred in Quark.

The context:  You tried to create a variable in a table;
The error:    The variable $name$ already exists;
What to do:   Please, find another name for a new variable;

Try following these steps:
    1.  Run `list variables in`;
    2.  Come up with a name for a new variable which is not in the list;
    3.  Rerun `create variable in`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.