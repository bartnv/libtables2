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
```php
  lt_table('users', 'All users', "SELECT id, name FROM users", [ 'sortable' => true ]);
```

See [lt_table() options](table_options_display/) for more information.

[^1]: in special cases you can pass in an array of column names instead of a query, to generate
a 'table' with no data but only insert fields

Insert-only example:
```php
  lt_table('users', 'Add user', [ 'id', 'name' ], [
    'insert' => [
      1 => [ 'users.name' ]
    ]
  ]);
```

## lt_print_block

Insert the contents of the specified Libtables block at this point in your website code.
The block can be simple HTML (using a .html file extension) or PHP/HTML (using a .php file
extension).

    lt_print_block(name, parameters)

Parameters:

  * name (required): the name of the block to use; libtables will search for this name, first
    with '.html' appended and, if not found, with .php appended, in the configured blocks_dir
  * parameters (optional): an array of parameters to be used from within the block (see [concepts](concepts/#parameters))

```php
  lt_print_block('productinfo', [ $_GET['product_id'] ]);
```

## lt_control [experimental]

The lt_control() function adds control-flow buttons to the current block.

    lt_control(tag, options)

Parameters:

  * tag (required): unique name for the controls within this block, only lowercase letters allowed
  * options (required): an array of options to specify the functionality of the buttons

```php
  lt_control('buttons', [
    'next' => [ 'payment', 'Go to payment' ],
    'verify' => "SELECT id FROM cart WHERE user = " . $_SESSION['user_id'],
    'error' => "you have no items in your cart"
  ]);
```

## lt_text [experimental]

The lt_text() function generates a text from a database query and adds it to the current block.
The text is live-updated by AJAX just as the tables are.

    lt_text(tag, query, parameters, format)

Parameters:

  * tag (required): unique name for the text within this block, only lowercase letters allowed
  * query (required): the SQL query generating the source data for this text (should only result in one row)
  * parameters (required): an array of parameters that can be used within the query (pass in an empty array if not required)
  * format (required): a format string; hashtags within this string will be replaced with the column values out of the query

```php
  lt_text('cartinfo',
    "SELECT SUM(amount) FROM cart WHERE user = ?",
    [ $_SESSION['user_id'] ],
    'Items in cart: #0'
  );
```
