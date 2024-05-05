#### Create a database

🔧 `create database` - creates a new database with a provided name.

##### Parameters

* 📦 `name` of type `str` - the name of a database;

##### Success message

```
✅  A new database $name$ was created. Now you can create tables with `create table "$name$.Table Name": columns = [];`
```

##### Reports

1. Database already exists
```
❌  An error occurred in Quark.

The context:  You was trying to create a database;
The error:    The database with the name $name$ already exists;
What to do:   Please, consider another name for your database;

Try following these steps:
    1.  Run `list databases`;
    2.  Come up with a name which is not in the list;
    3.  Rerun `create database` with a new name;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. Database cannot have a OS-reserved name
```
❌  An error occurred in Quark.

The context:  You was trying to create a database;
The error:    The $name$ is a reserved Windows file name;
What to do:   Please, consider another name for your database;

Try following these steps:
    1.  Open Microsoft article: https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file;
    2.  Find the list of reserved file names;
    3.  Come up with a name which is not in the list;
    4.  Rerun `create database` with a new name;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

3. Database folder path would be too long `🪟 Windows only`
```
❌  An error occurred in Quark.

The context:  You was trying to create a database;
The error:    The path would be too long;
What to do:   Please, move the Databases folder somewhere higher in your file system;

Try following these steps:
    1.  Find a new folder for Databases folder;
    2.  Copy the path to the folder you've chosen. It must be shorter than 256 characters;
    3.  Run `move databases folder to "PASTE PATH HERE";`;


Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.