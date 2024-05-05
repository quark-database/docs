<p align="center">
    <a href="https://anafro.ru/quark">
        <img src="https://raw.githubusercontent.com/quark-database/.github/main/Assets/Banner.png" alt="Quark Banner">
    </a>
</p>

<h1 align="left">About Quark Documentation</h1>

The Quark Documentation describes not the actual implementation of Quark, but the specification of Quark products. Effectively this is a set of guidelines about how to create your own Quark!

<details open>
<summary><kbd>Table of contents</kbd></summary>

- [📁 Databases in File System](#-databases-in-file-system)
  - [The capitalized case](#the-capitalized-case)
  - [Databases](#databases)
  - [Tables](#tables)
  - [Table records](#table-records)
  - [Table header](#table-header)
  - [Records](#records)
  - [Table variables](#table-variables)
- [📚 Database Management Specification](#-database-management-specification)
  - [Operations for databases](#operations-for-databases)
    - [Rename a database](#rename-a-database)
      - [Parameters](#parameters)
      - [Success message](#success-message)
      - [Reports](#reports)
      - [Result](#result)
    - [List databases](#list-databases)
      - [Parameters](#parameters-1)
      - [Success message](#success-message-1)
      - [Reports](#reports-1)
      - [Result](#result-1)
    - [Clone a database](#clone-a-database)
      - [Parameters](#parameters-2)
      - [Success message](#success-message-2)
      - [Reports](#reports-2)
      - [Result](#result-2)
    - [Clone a database skeleton](#clone-a-database-skeleton)
    - [List tables in a database](#list-tables-in-a-database)
    - [Clear a database](#clear-a-database)
    - [Delete a database](#delete-a-database)
  - [Operations for tables](#operations-for-tables)
    - [Create a table](#create-a-table)
    - [Rename a table](#rename-a-table)
    - [List tables](#list-tables)
    - [Clone a table](#clone-a-table)
    - [Clone a table skeleton](#clone-a-table-skeleton)
    - [List tables in a table](#list-tables-in-a-table)
    - [Clear a table](#clear-a-table)
    - [Delete a table](#delete-a-table)
  - [Operations for records](#operations-for-records)
    - [Change records](#change-records)
    - [Count records](#count-records)
    - [Insert a record](#insert-a-record)
    - [Select a record](#select-a-record)
    - [Delete records](#delete-records)
  - [Operations for columns](#operations-for-columns)
    - [Create a column](#create-a-column)
    - [Rename a column](#rename-a-column)
    - [Swap columns](#swap-columns)
    - [Reorder columns](#reorder-columns)
    - [List columns](#list-columns)
    - [Delete a column](#delete-a-column)
  - [Operations for variables](#operations-for-variables)
    - [Create a variable](#create-a-variable)
    - [Get a variable value](#get-a-variable-value)
    - [Set a variable value](#set-a-variable-value)
    - [List variables in a table](#list-variables-in-a-table)
    - [Delete a variable](#delete-a-variable)
  - [Operations for auth tokens](#operations-for-auth-tokens)
    - [Create a token](#create-a-token)
    - [Grant a permission to a token](#grant-a-permission-to-a-token)
    - [Revoke a permission to a token](#revoke-a-permission-to-a-token)
    - [Redefine permissions for a token](#redefine-permissions-for-a-token)
    - [Delete a token](#delete-a-token)
  - [Operations for a cloud](#operations-for-a-cloud)
    - [Get a server name](#get-a-server-name)
    - [Rename a server](#rename-a-server)
    - [Evaluate Quark expression](#evaluate-quark-expression)
    - [Change the server port](#change-the-server-port)
    - [Secret instruction](#secret-instruction)
- [✍️ Query Language Specification](#️-query-language-specification)
- [❌ Error Specification](#-error-specification)
  - [Reports](#reports-3)

</details>

## 📁 Databases in File System

**Quark** is a relational database management system. It means that the instance of Quark DBMS contains multiple databases with tables inside. Every element, which is any named entity inside Quark, including databases, tables, etc., of the Quark DBMS hierarchy must be named in a special capitalized case.

### The capitalized case

**The capitalized case** used in Quark naming requires words to be capitalized and separated with spaces. The words must only contain latin letters, and digits. Words are allowed to be uppercase, but only if they are abbreviations. 

### Databases

**A database** is a named set of tables. In Quark, each database is a folder. The folder name is considered to be the name of database. All the databases must be stored in one folder (canonically named `Databases`). Every folder inside the database is considered to be a table of this database. 

### Tables

**A table** is a named set of records, and information about columns. A table, like databases, is a folder, which is contained by a database. A table is structured the following way:

```
My Database                     <-- The database folder
|
|---- Users                     <-- The table folder
    |
    |---- Variables             <-- The variables folder
    |   |
    |   |---- Next Id.qvar
    |   |---- Next Token.qvar
    |   |---- ...
    |
    |---- Records.qrecs         <-- The records file of the table
    |---- Header.qhead          <-- The header file of the table
```

Any other file or folder must be ignored.

### Table records

**The table records file** contains all the records. Each line of the file represents one record. 

```
// Records.qrecs
"1","Anatoly",22
"2","Aleksandr",21
"3","Egor",22
```

### Table header

**The table header file** contains names of the table column and their types. Each line of table header contains the type, name, and the properties of the columns. The property list can be empty.

```
// Header.qhead:
int("Id", incrementing)
str("Name")
int("Age", positive)

int                                         ("Id",                                  incrementing)
^                                            ^                                      ^
| Type of column (here, it is integer)       | The column name (here, it is Id)     | The list of properties (here, it is one property: incrementing)
 \____________________________________        \________________________________      \______________________________________________________________
```

The column definition is a Quark query language expression. <a href="#expressions">Learn more about Quark QL expressions</a>.

### Records

**A record** is a set of cells. Each record contains zero, one, or more values called cells. Effectively each cell is named because of the table header:

```
// Header.qhead:
int("Id", incrementing)
str("Name")
int("Age", positive)

// Records.qrecs
"1","Anatoly",22
"2","Aleksandr",21
"3","Egor",22


1,                              "Anatoly",                    22
^                               ^                             ^
| Considered to be an Id.       | Considered to be a Name.    | Considered to be an Age.
 \_________________________      \_____________________        \_________________________________
```

**A record inside a record file** is several double-quoted strings separated with commas:

```
"this is a string","123","true"
```

Even though some strings can be stored without quotes, and be not misrecognized (for example, `"strings without commas"`), they must be double-quoted anyways. The quotation mark can be stored into a cell via escaping:
```
                              V              V Just put the backslash in front of the symbols to espace them!
...,"Hi, do you know the book \"War and Peace\"?",...
```

Besides the quotation marks, there is a line break (`\n`) that can be escaped. To store backslash itself, escape it (`\\`).
Any other character cannot be escaped, and is an error.

Inside one table, each record must contain an equal count of cells, same as columns in the table header. It means that the following example is an error:

```
// Header.qhead:
int("Id", incrementing)
str("Name")
int("Age", positive)

// Records.qrecs
"1","Anatoly",22,"Hello"    <-- ❌ The 4th cell is redundant.
"2","Aleksandr"             <-- ❌ The 3rd cell is missing.
"3","Egor",22               <-- ✅ Ok!
```

### Table variables

**A table variable** contains only one value (for example, a string or an integer). At this moment, in Quark `v4.0`, table variables are only used for the `incrementing` property to store the next integer value for an incrementing column, but variables is a great feature with many undiscovered possibilities.

**A table variable file** contains one line - a Quark expression. <a href="#expressions">Learn more about Quark QL expressions</a>.

All the table variable files are stored inside the `Variables` folder inside the table folder.

```
// Next Id.qvar
100                         <-- 100 will be taken as an Id for the next insertion. 
```

## 📚 Database Management Specification

A user can perform operations on databases, tables, records, columns, variables, auth tokens, and a cloud.

### Operations for databases


#### Rename a database

🔧 `rename database` - renames a database.

##### Parameters

* 📦 `name` of type `str` - the name of a database;
* 📦 `to` of type `str` - a new name of the database;

##### Success message

```
✅  The database $name$ is now named $newname$.`
```

##### Reports

1. Database already exists
```
❌  An error occurred in Quark.

The context:  You was trying to rename a database $name$ to $newname$;
The error:    The database with the name $newname$ already exists;
What to do:   Please, consider another name for your database;

Try following these steps:
    1.  Run `list databases`;
    2.  Come up with a name which is not in the list;
    3.  Rerun `rename database` with a new name;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. Database cannot have a OS-reserved name
```
❌  An error occurred in Quark.

The context:  You was trying to rename a database $name$ to $newname$;
The error:    The $newname$ is a reserved Windows file name;
What to do:   Please, consider another name for your database;

Try following these steps:
    1.  Open Microsoft article: https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file
    2.  Find the list of reserved file names.
    3.  Come up with a name which is not in the list.
    4.  Rerun `create database` with a new name.

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

3. Database folder path would be too long `🪟 Windows only`
```
❌  An error occurred in Quark.

The context:  You was trying to rename a database $name$ to $newname$;
The error:    The path would be too long;
What to do:   Please, move the Databases folder somewhere higher in your file system;

Try following these steps:
    1.  Find a new folder for Databases folder.
    2.  Copy the path to the folder you've chosen. It must be shorter than 256 characters.
    3.  Run `move databases folder to "PASTE PATH HERE";`.


Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

🚫 This instruction returns no result.

#### List databases

🔧 `list databases` - lists all the databases.

##### Parameters

🚫 This instruction takes no parameters.

##### Success message

```
✅  The database $name$ is now named $newname$.`
```

##### Reports

1. Database already exists
```
❌  An error occurred in Quark.

The context:  You was trying to rename a database $name$ to $newname$;
The error:    The database with the name $newname$ already exists;
What to do:   Please, consider another name for your database;

Try following these steps:
    1.  Run `list databases`;
    2.  Come up with a name which is not in the list;
    3.  Rerun `rename database` with a new name;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. Database cannot have a OS-reserved name
```
❌  An error occurred in Quark.

The context:  You was trying to rename a database $name$ to $newname$;
The error:    The $newname$ is a reserved Windows file name;
What to do:   Please, consider another name for your database;

Try following these steps:
    1.  Open Microsoft article: https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file
    2.  Find the list of reserved file names.
    3.  Come up with a name which is not in the list.
    4.  Rerun `create database` with a new name.

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

3. Database folder path would be too long `🪟 Windows only`
```
❌  An error occurred in Quark.

The context:  You was trying to rename a database $name$ to $newname$;
The error:    The path would be too long;
What to do:   Please, move the Databases folder somewhere higher in your file system;

Try following these steps:
    1.  Find a new folder for Databases folder.
    2.  Copy the path to the folder you've chosen. It must be shorter than 256 characters.
    3.  Run `move databases folder to "PASTE PATH HERE";`.


Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

##### Result

|  `Database name` of type `str`  |
|:-------------------------------:|
| The database names of the cloud |

#### Clone a database

🔧 `clone database` - lists all the databases.

##### Parameters

* 📦 `name` of type `str` - the name of a database;
* 📦 `to` of type `str` - a new name of the database;

##### Success message

```
✅  The database $name$ is now named $newname$.`
```

##### Reports

1. Database already exists
```
❌  An error occurred in Quark.

The context:  You was trying to rename a database $name$ to $newname$;
The error:    The database with the name $newname$ already exists;
What to do:   Please, consider another name for your database;

Try following these steps:
    1.  Run `list databases`;
    2.  Come up with a name which is not in the list;
    3.  Rerun `rename database` with a new name;

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

2. Database cannot have a OS-reserved name
```
❌  An error occurred in Quark.

The context:  You was trying to rename a database $name$ to $newname$;
The error:    The $newname$ is a reserved Windows file name;
What to do:   Please, consider another name for your database;

Try following these steps:
    1.  Open Microsoft article: https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file
    2.  Find the list of reserved file names.
    3.  Come up with a name which is not in the list.
    4.  Rerun `create database` with a new name.

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```

3. Database folder path would be too long `🪟 Windows only`
```
❌  An error occurred in Quark.

The context:  You was trying to rename a database $name$ to $newname$;
The error:    The path would be too long;
What to do:   Please, move the Databases folder somewhere higher in your file system;

Try following these steps:
    1.  Find a new folder for Databases folder.
    2.  Copy the path to the folder you've chosen. It must be shorter than 256 characters.
    3.  Run `move databases folder to "PASTE PATH HERE";`.


Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```


##### Result

|  `Database name` of type `str`  |
|:-------------------------------:|
| The database names of the cloud |

#### Clone a database skeleton

#### List tables in a database

#### Clear a database

#### Delete a database

### Operations for tables

#### Create a table

#### Rename a table

#### List tables

#### Clone a table

#### Clone a table skeleton

#### List tables in a table

#### Clear a table

#### Delete a table

### Operations for records

#### Change records

#### Count records

#### Insert a record

#### Select a record

#### Delete records

### Operations for columns

#### Create a column

#### Rename a column

#### Swap columns

#### Reorder columns

#### List columns

#### Delete a column

### Operations for variables

#### Create a variable

#### Get a variable value

#### Set a variable value

#### List variables in a table

#### Delete a variable

### Operations for auth tokens

#### Create a token

#### Grant a permission to a token

#### Revoke a permission to a token

#### Redefine permissions for a token

#### Delete a token

### Operations for a cloud

#### Get a server name

#### Rename a server

#### Evaluate Quark expression

#### Change the server port

#### Secret instruction

## ✍️ Query Language Specification

> [!CAUTION]
> 🚧 The query language specification will soon be defined.

## ❌ Error Specification

**Errors** must be descriptive in any computer system due to their purpose: describe the problem and help to find a fixing solution. The errors in Quark are based on reports.

### Reports

**A report** is an extension for exceptions, which contains more information about the problematic situation. Besides the error message, there are several messages in it in addition:

* **A context** is an environment of the situation, in what circumstances the problem was born. For example, `The calculator was trying to calculate the expression value`.
* **An error message** is a good old exception message. Describe here the situation, the error itself. For example, `The division by zero is prohibited`. 
* **A piece of advice** is what a user should do to fix the problem. `Please, do not enter zeros for the division operator.`
* **Fix steps** are the steps to fix the problem. In other words, it is a piece of advice, but split to a set of steps. Since a piece of advice is enough, an empty list of steps can be passed.

For example, this is how a string formatted report would look:

```
❌  An error occurred in Quark.

The context:  The server was trying to launch;
The error:    The port is configuration is missing;
What to do:   Please, add the port to a configuration;

Try following these steps:
    1.  Open the configuration file `D:/Quark Cloud/Configuration.json`
    2.  Find the `port` option (if it's not here, add it)
    3.  Set the `port` to any port you would like to use (I recommend to set it to 10000).

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```