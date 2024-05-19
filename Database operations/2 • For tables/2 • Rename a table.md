#### Rename a table

🔧 `rename table` - renames a table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;
* 📦 `to` of type `str` - the new name of a table;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The table has been renamed.
```

##### Reports

1. Table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to rename a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you did not misspell it;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find a table you want to rename;
    3.  Rerun `rename table`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

1. Table already exists
```
❌  An error occurred in Quark.

The context:  You tried to rename a table;
The error:    There already is a table with name $name$;
What to do:   Please, ensure that you did not misspell the new name;

Try following these steps:
    1.  Run `list tables in`;
    2.  Come up with a table name that is not in the list;
    3.  Rerun `rename table`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.