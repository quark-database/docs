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
    - [🔧 Create a database](#-create-a-database)
    - [🔧 Rename a database](#-rename-a-database)
    - [🔧 List databases](#-list-databases)
    - [🔧 Clone a database](#-clone-a-database)
    - [🔧 Clone a database skeleton](#-clone-a-database-skeleton)
    - [🔧 List tables in a database](#-list-tables-in-a-database)
    - [🔧 Clear a database](#-clear-a-database)
    - [🔧 Delete a database](#-delete-a-database)
  - [Operations for tables](#operations-for-tables)
    - [🔧 Create a table](#-create-a-table)
    - [🔧 Rename a table](#-rename-a-table)
    - [🔧 Clone a table](#-clone-a-table)
    - [🔧 Clone a table skeleton](#-clone-a-table-skeleton)
    - [🔧 Clear a table](#-clear-a-table)
    - [🔧 Delete a table](#-delete-a-table)
  - [Operations for records](#operations-for-records)
    - [🔧 Change records](#-change-records)
    - [🔧 Count records](#-count-records)
    - [🔧 Insert a record](#-insert-a-record)
    - [🔧 Select records](#-select-records)
    - [🔧 Delete records](#-delete-records)
  - [Operations for columns](#operations-for-columns)
    - [🔧 Create a column](#-create-a-column)
    - [🔧 Rename a column](#-rename-a-column)
    - [🔧 Swap columns](#-swap-columns)
    - [🔧 Reorder columns](#-reorder-columns)
    - [🔧 List columns](#-list-columns)
    - [🔧 Delete a column](#-delete-a-column)
  - [Operations for variables](#operations-for-variables)
    - [🔧 Create a variable](#-create-a-variable)
    - [🔧 Get a variable value](#-get-a-variable-value)
    - [🔧 Set a variable value](#-set-a-variable-value)
    - [🔧 List variables in a table](#-list-variables-in-a-table)
    - [🔧 Delete a variable](#-delete-a-variable)
  - [Operations for tokens](#operations-for-tokens)
    - [🔧 Create a token](#-create-a-token)
    - [🔧 Grant a permission to a token](#-grant-a-permission-to-a-token)
    - [🔧 Revoke a permission from a token](#-revoke-a-permission-from-a-token)
    - [🔧 Redefine permissions for a token](#-redefine-permissions-for-a-token)
    - [🔧 Delete a token](#-delete-a-token)
  - [Operations for the cloud](#operations-for-the-cloud)
    - [🔧 Get a cloud name](#-get-a-cloud-name)
    - [🔧 Rename a cloud](#-rename-a-cloud)
    - [🔧 Evaluate expression](#-evaluate-expression)
    - [🔧 Change the cloud port](#-change-the-cloud-port)
    - [🔧 Secret](#-secret)
- [✍️ Query Language Specification](#️-query-language-specification)
- [❌ Error Specification](#-error-specification)
  - [Reports](#reports)

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

#### [🔧 Create a database](https://github.com/quark-database/docs/blob/main/Database%20operations/1%20%E2%80%A2%20For%20databases/1%20%E2%80%A2%20Create%20a%20database.md)
#### [🔧 Rename a database](https://github.com/quark-database/docs/blob/main/Database%20operations/1%20%E2%80%A2%20For%20databases/2%20%E2%80%A2%20Rename%20a%20database.md)
#### [🔧 List databases](https://github.com/quark-database/docs/blob/main/Database%20operations/1%20%E2%80%A2%20For%20databases/3%20%E2%80%A2%20List%20databases.md)
#### [🔧 Clone a database](https://github.com/quark-database/docs/blob/main/Database%20operations/1%20%E2%80%A2%20For%20databases/4%20%E2%80%A2%20Clone%20a%20database.md)
#### [🔧 Clone a database skeleton](https://github.com/quark-database/docs/blob/main/Database%20operations/1%20%E2%80%A2%20For%20databases/5%20%E2%80%A2%20Clone%20a%20database%20skeleton.md)
#### [🔧 List tables in a database](https://github.com/quark-database/docs/blob/main/Database%20operations/1%20%E2%80%A2%20For%20databases/6%20%E2%80%A2%20List%20tables%20in%20a%20database.md)
#### [🔧 Clear a database](https://github.com/quark-database/docs/blob/main/Database%20operations/1%20%E2%80%A2%20For%20databases/7%20%E2%80%A2%20Clear%20a%20database.md)
#### [🔧 Delete a database](https://github.com/quark-database/docs/blob/main/Database%20operations/1%20%E2%80%A2%20For%20databases/8%20%E2%80%A2%20Delete%20a%20database.md)

### Operations for tables

#### [🔧 Create a table](https://github.com/quark-database/docs/blob/main/Database%20operations/2%20%E2%80%A2%20For%20tables/1%20%E2%80%A2%20Create%20a%20table.md)
#### [🔧 Rename a table](https://github.com/quark-database/docs/blob/main/Database%20operations/2%20%E2%80%A2%20For%20tables/2%20%E2%80%A2%20Rename%20a%20table.md)
#### [🔧 Clone a table](https://github.com/quark-database/docs/blob/main/Database%20operations/2%20%E2%80%A2%20For%20tables/3%20%E2%80%A2%20Clone%20a%20table.md)
#### [🔧 Clone a table skeleton](https://github.com/quark-database/docs/blob/main/Database%20operations/2%20%E2%80%A2%20For%20tables/4%20%E2%80%A2%20Clone%20a%20table%20skeleton.md)
#### [🔧 Clear a table](https://github.com/quark-database/docs/blob/main/Database%20operations/2%20%E2%80%A2%20For%20tables/5%20%E2%80%A2%20Clear%20a%20table.md)
#### [🔧 Delete a table](https://github.com/quark-database/docs/blob/main/Database%20operations/2%20%E2%80%A2%20For%20tables/6%20%E2%80%A2%20Delete%20a%20table.md)

### Operations for records

#### [🔧 Change records](https://github.com/quark-database/docs/blob/main/Database%20operations/3%20%E2%80%A2%20For%20records/1%20%E2%80%A2%20Change%20records.md)
#### [🔧 Count records](https://github.com/quark-database/docs/blob/main/Database%20operations/3%20%E2%80%A2%20For%20records/2%20%E2%80%A2%20Count%20records.md)
#### [🔧 Insert a record](https://github.com/quark-database/docs/blob/main/Database%20operations/3%20%E2%80%A2%20For%20records/3%20%E2%80%A2%20Insert%20a%20record.md)
#### [🔧 Select records](https://github.com/quark-database/docs/blob/main/Database%20operations/3%20%E2%80%A2%20For%20records/4%20%E2%80%A2%20Select%20records.md)
#### [🔧 Delete records](https://github.com/quark-database/docs/blob/main/Database%20operations/3%20%E2%80%A2%20For%20records/5%20%E2%80%A2%20Delete%20records.md)

### Operations for columns

#### [🔧 Create a column](https://github.com/quark-database/docs/blob/main/Database%20operations/4%20%E2%80%A2%20For%20columns/1%20%E2%80%A2%20Create%20a%20column.md)
#### [🔧 Rename a column](https://github.com/quark-database/docs/blob/main/Database%20operations/4%20%E2%80%A2%20For%20columns/2%20%E2%80%A2%20Rename%20a%20column.md)
#### [🔧 Swap columns](https://github.com/quark-database/docs/blob/main/Database%20operations/4%20%E2%80%A2%20For%20columns/3%20%E2%80%A2%20Swap%20columns.md)
#### [🔧 Reorder columns](https://github.com/quark-database/docs/blob/main/Database%20operations/4%20%E2%80%A2%20For%20columns/4%20%E2%80%A2%20Reorder%20columns.md)
#### [🔧 List columns](https://github.com/quark-database/docs/blob/main/Database%20operations/4%20%E2%80%A2%20For%20columns/5%20%E2%80%A2%20List%20columns.md)
#### [🔧 Delete a column](https://github.com/quark-database/docs/blob/main/Database%20operations/4%20%E2%80%A2%20For%20columns/6%20%E2%80%A2%20Delete%20a%20column.md)

### Operations for variables

#### [🔧 Create a variable](https://github.com/quark-database/docs/blob/main/Database%20operations/5%20%E2%80%A2%20For%20variables/1%20%E2%80%A2%20Create%20a%20variable.md)
#### [🔧 Get a variable value](https://github.com/quark-database/docs/blob/main/Database%20operations/5%20%E2%80%A2%20For%20variables/2%20%E2%80%A2%20Get%20a%20variable%20value.md)
#### [🔧 Set a variable value](https://github.com/quark-database/docs/blob/main/Database%20operations/5%20%E2%80%A2%20For%20variables/3%20%E2%80%A2%20Set%20a%20variable%20value.md)
#### [🔧 List variables in a table](https://github.com/quark-database/docs/blob/main/Database%20operations/5%20%E2%80%A2%20For%20variables/4%20%E2%80%A2%20List%20variables%20in%20a%20table.md)
#### [🔧 Delete a variable](https://github.com/quark-database/docs/blob/main/Database%20operations/5%20%E2%80%A2%20For%20variables/5%20%E2%80%A2%20Delete%20a%20variable.md)

### Operations for tokens

#### [🔧 Create a token](https://github.com/quark-database/docs/blob/main/Database%20operations/6%20%E2%80%A2%20For%20auth%20tokens/1%20%E2%80%A2%20Create%20a%20token.md)
#### [🔧 Grant a permission to a token](https://github.com/quark-database/docs/blob/main/Database%20operations/6%20%E2%80%A2%20For%20auth%20tokens/2%20%E2%80%A2%20Grant%20a%20permission%20to%20a%20token.md)
#### [🔧 Revoke a permission from a token](https://github.com/quark-database/docs/blob/main/Database%20operations/6%20%E2%80%A2%20For%20auth%20tokens/3%20%E2%80%A2%20Revoke%20a%20permission%20from%20a%20token.md)
#### [🔧 Redefine permissions for a token](https://github.com/quark-database/docs/blob/main/Database%20operations/6%20%E2%80%A2%20For%20auth%20tokens/4%20%E2%80%A2%20Redefine%20permissions%20for%20a%20token.md)
#### [🔧 Delete a token](https://github.com/quark-database/docs/blob/main/Database%20operations/6%20%E2%80%A2%20For%20auth%20tokens/5%20%E2%80%A2%20Delete%20a%20token.md)

### Operations for the cloud

#### [🔧 Get a cloud name](https://github.com/quark-database/docs/blob/main/Database%20operations/7%20%E2%80%A2%20For%20a%20cloud/1%20%E2%80%A2%20Get%20a%20cloud%20name.md)
#### [🔧 Rename a cloud](https://github.com/quark-database/docs/blob/main/Database%20operations/7%20%E2%80%A2%20For%20a%20cloud/2%20%E2%80%A2%20Rename%20a%20cloud.md)
#### [🔧 Evaluate expression](https://github.com/quark-database/docs/blob/main/Database%20operations/7%20%E2%80%A2%20For%20a%20cloud/3%20%E2%80%A2%20Evaluate%20expression.md)
#### [🔧 Change the cloud port](https://github.com/quark-database/docs/blob/main/Database%20operations/7%20%E2%80%A2%20For%20a%20cloud/4%20%E2%80%A2%20Change%20the%20cloud%20port.md)
#### [🔧 Secret](https://github.com/quark-database/docs/blob/main/Database%20operations/7%20%E2%80%A2%20For%20a%20cloud/5%20%E2%80%A2%20Secret.md)


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