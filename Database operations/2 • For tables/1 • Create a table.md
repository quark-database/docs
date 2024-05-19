#### Create a table

🔧 `create table` - creates a new table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;
* 📦 `columns` of type `array of columns` - the columns of a table;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The table has been successfully created.
```

##### Reports

1. Table already exists
```
❌  An error occurred in Quark.

The context:  You tried to create a table;
The error:    The table $name$ already exists;
What to do:   Please, ensure that you didn't misspell the name;

Try following these steps:
    1.  Run `list tables in`;
    2.  Run `create table` with a correct table name; 

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. Column list is empty
```
❌  An error occurred in Quark.

The context:  You tried to create a table;
The error:    The table $name$ must have at least one column;
What to do:   Please, ensure add at least one column;

Try following these steps:
    1.  Run `create table` and add a column to array passed to `columns` parameter; 

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.