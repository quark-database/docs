#### List tables in a database

🔧 `list tables in` - lists all the tables in a database.

##### Parameters

* 📦 `name` of type `str` - the name of a database;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  This is the list of all databases.
```

##### Reports

1. Database does not exist
```
❌  An error occurred in Quark.

The context:  You was trying to get the list of all the tables inside $name$;
The error:    The database $name$ does not exist;
What to do:   Please, ensure that you spelled the database name correctly;

Try following these steps:
    1.  Run `list databases`;
    2.  Find if there is a database you wanted;
    3.  Rerun `list tables in` with a correct name;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

|                `Table Name` of type `str`                 |
|:---------------------------------------------------------:|
| All the names of the tables inside the requested database |

<!-- or...
🚫 This instruction returns no result.
-->