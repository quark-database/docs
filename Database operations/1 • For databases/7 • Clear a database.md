#### Clear a database

🔧 `clear database` - removes all the tables from a database.

##### Parameters

* 📦 `name` of type `str` - the name of a database;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The database was cleared, and now has no tables inside.
```

##### Reports

1. Database does not exist
```
❌  An error occurred in Quark.

The context:  You tried to clear a database;
The error:    The database $name$ does not exist;
What to do:   Please, ensure its name, it is possibly misspelled;

Try following these steps:
    1.  Run `list databases`;
    2.  Find a database you want to clear;
    3.  Run `clear database` again;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.