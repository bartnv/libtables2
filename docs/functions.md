# Libtables Functions

## lt_table

The lt_table() function adds a table to the current block.

    lt_table(tag, title, query, options)

Parameters:

  * tag (required): unique name for the table within this block, only lowercase letters allowed
  * title (required): name of the table, displayed within a <th> tag at the top
  * query (required): the SQL query to generate the rows for this table[^1]
  * options (optional): an array of options to add functionality such as insert, delete, edit-in-place,
    filtering, sorting, etc to your table

Basic example:
```
    lt_table('users', 'All users', "SELECT id, name FROM users", [ 'sortable' => true ]);
```

See [lt_table() options](table_function/) for more information.

[^1]: in special cases you can pass in an array of column names instead of a query, to generate
a 'table' with no data but only insert fields

## lt_control

## lt_text
