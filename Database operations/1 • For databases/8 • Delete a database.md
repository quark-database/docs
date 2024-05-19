#### Delete a database

🔧 `delete database` - deletes a database.

##### Parameters

* 📦 `name` of type `str` - the name of a database;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The database has been deleted.
```

##### Reports

1. Database does not exist
```
❌  An error occurred in Quark.

The context:  You tried to delete a database;
The error:    Database $name$ does not exist;
What to do:   Please, ensure that your database exists;

Try following these steps:
    1.  Run `list databases`;
    2.  Find a database you want to delete;
    3.  Run `delete database` with a correct database name;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.