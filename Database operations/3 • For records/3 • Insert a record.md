#### Insert a record

🔧 `insert into` - inserts a new record into a table.

##### Parameters

* 📦 `name` of type `str` - the name of a table;
* 📦 `record` of type `record` - the record to insert;

<!-- or...
🚫 This instruction takes no parameters.
-->

##### Success message

```
✅  The record has been inserted.
```

##### Reports

1. Table does not exist
```
❌  An error occurred in Quark.

The context:  You tried to insert a record into a table;
The error:    The table $name$ does not exist;
What to do:   Please, ensure that you did not misspell it;

Try following these steps:
    1.  Run `list tables in`;
    2.  Find a table you want to insert the record into;
    3.  Rerun `insert into`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. Record does not match the table columns
```
❌  An error occurred in Quark.

The context:  You tried to insert a record into a table;
The error:    The record does not match the table columns;
What to do:   Check what columns are wrong or missing;

Try following these steps:
    1.  Run `list columns in`;
    2.  Look at the column list;
    3.  Check the values in your record;
    4.  Edit the record;
    5.  Rerun `insert into`;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.