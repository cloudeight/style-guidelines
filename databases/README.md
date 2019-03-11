# Style Guidelines: Databases
> *A set of guidelines to databases...*
<br />


## Table of Contents
1. [Naming Conventions](#naming-conventions)
    - [General](#general)
    - [Tables](#tables)
    - [Columns](#columns)
    - [Primary Keys](#primary-keys)
    - [Foreign Keys](#foreign-keys)
    - [Map/Pivot Tables](#mappivot-tables)
    - [Constraints](#constraints)
2. [Character Encoding](#character-encoding)
3. [Dates](#dates)
4. [SQL](#sql)


## Naming Conventions
### General
Always ensure that no reserved keywords are used when naming tables and columns, refer to [this list](https://www.drupal.org/docs/develop/coding-standards/list-of-sql-reserved-words) by Drupal for a list of all the reserved keywords.

### Tables
Tables are a collection of one (1) or more rows/entities, table names should:

- Use lowercase
- Use snake_case
- Be defined in the plural

```
// Users table
users

// User sessions table
user_sessions
```

Please refer to the [map/pivot tables](#mappivot-tables) section for more on many to many relationship tables.


### Columns
Column names should:

- Use lowercase
- Use snake_case

```
// First name
first_name

// Date of birth
date_of_birth
```

### Primary Keys
Every table should have a unique identifier column, set as a primary key that auto increments, this row should simply be called `id`.

Please refer to the [constraints](#constraints) section for more on naming primary key constraints.

### Foreign Keys
When referencing a primary key in another table, a foreign key should:

- Use lowercase
- Use snake_case
- Use the singular form of the table it is referencing
- Be suffixed with the referenced tables primary key column name

```
// Users table primary key
id

// Posts table referencing a user
user_id
```

Please refer to the [constraints](#constraints) section for more on naming foreign key constraints.

### Map/Pivot Tables
If a tables primary purpose is to define many to many relationships, the table name should:

- Use lowercase
- Use snake_case
- List table names alphabetically
- Define table names in the singular
- Be suffixed with the word `maps`
    - Conforming to the pluralized requirements listed [above](#tables)

```
// Users and posts
post_user_maps

// Users and comments
comment_user_maps

// Posts and comments
comment_post_maps
```

As with any table, this table must have a [primary key](#primary-keys), along with the [foreign keys](#foreign-keys) of each table in the many to many relationship.

```
// Users and posts
id | post_id | user_id

// Users and comments
id | comment_id | user_id

// Posts and comments
id | comment_id | post_id
```

### Constraints
With the exception of primary keys, all constraints should:

- Use lowercase
- Use snake_case
- Use the following order:
    - Table name
    - Column name
    - Constraint name character suffix

Taking the users and posts examples, using a many to many relationship, the `post_id` and `user_id` foreign keys would have the following naming conventions:

```
// Users table
users

// Users table primary key
id

// Posts table
posts

// Posts table primary key
id

// Map/Pivot table
post_user_maps

// Map/Pivot table columns
id | post_id | user_id

// Map/Pivot tables post_id foreign key constraint
post_user_maps_post_id_fk

// Map/Pivot tables user_id foreign key constraint
post_user_maps_user_id_fk
```
As mentioned, primary keys are the only exception to the constraint naming conventions, primary key constraint names should:

- Use lowercase
- Use snake_case
- Use the following order:
    - Table name
    - Primary key constraint character suffix

```
users_pk
```

Here is a list of all the constraints and their corresponding character suffixes:

| Constraint  | Character Suffix |
|-------------|------------------|
| Primary Key | _pk              |
| Foreign Key | _fk              |
| Check       | _ck              |
| Not Null    | _nn              |
| Unique      | _uq              |
| Index       | _in              |


## Character Encoding
This section is not necessarily for the general public to follow unless you wish to, this is more of a reference for [cloudeight](https://github.com/cloudeight) in-house projects. Here at [cloudeight](https://github.com/cloudeight) we predominantly use the following character encoding:

- Character Set: `utf8mb4`
- Collation: `utf8mb4_unicode_ci`

Obviously this can be adjusted on a per project basis but it is a good starting point.


## Dates
Just like the [character encoding](#character-encoding), this is more of a reference for [cloudeight](https://github.com/cloudeight) in-house projects.

We include a `created_at`, `updated_at` and `deleted_at` column on every table, with the exception of [map/pivot tables](#mappivot-tables). Each of these columns is stored using the `TIMESTAMP` datatype. These columns  allow us to have a reference of when the row was inserted and updated. The `deleted_at` column is used at times when we don't want to completely remove an entry from a table, this is called soft deletion or soft deleting.

It allows us to filter out "deleted" entries to a table in our queries, while also knowing when it was "deleted" and allowing for it to be restored if necessary, think of it as a recycle bin for table rows/entries.

Obviously this can be adjusted on a per project basis but it is a good starting point.


## SQL
Now that we have established naming conventions and structuring of our databases, it would be a good time to follow on from this by reading our SQL style guidelines. However, unfortunately this part of our style guidelines is still a work in progress and should hopefully be published soon.
