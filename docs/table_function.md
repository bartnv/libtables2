# Parameters

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

[^1]: in special cases you can pass in an array of column names instead of a query, to generate
a 'table' with no data but only insert fields

# Display options

## sortable

**sortable** (boolean): set to true to add sorting functionality to the column headers
    This setting doesn't affect (or even know) the initial sorting order of the data, which is
    specified in the SQL query.
```
    [ 'sortable' => true ]
```
## filter
  * filter (boolean): add a filter row just below the headers of the table. Filter fields for numeric fields
    accept numeric logic like "< 4" or "= 10". Filter fields for text columns support regular expression matching
    like "(red|green)" or "^start". Multiple fields combine with AND logic. The filter icon at the top left of the
    table briefly lists these capabilities in its mouseover text.
```
    [ 'filter' => true ]
```
## limit
  * limit (integer): limit the table to x rows and add pagination controls to page through the results
```
    [ 'limit ' => 25 ]
```

  * pagename (string): only used with limit or format; substitutes the text 'Page' in the pagination controls created by the 'limit' option
    at the top of the table with the contents of this field
```
    [ 'pagename' => 'YourText' ]
```


  * hideheader (boolean): hides the top row of header names
```
    [ 'hideheader' => true ]
```

* sum (array): adds one or more summation fields at the bottom of the specified column(s)

  The example below adds a sum at the bottom of columns 1 and 3, but only if these columns are indeed numeric.
```
    [
      'sum' => [
        1 => true,
        3 => true
      ]
    ]
```

  * mouseover (array) #

  * hidecolumn (array) #

  * showid (boolean)

  * classes (array) table/#

  * style (array) list/selectone

  * transformations (array) # image/round

  * format (string)

  * pagetitle (string with #-replacement)

  * emptycelltext (string)

  * textifempty (string)

  * hideifempty (boolean)

  * appendcell (string)

  * appendrow (string)

  * subtables (array) #

  * display (string)

  * rowlink (string): only used for display => divs

  * trigger (string)

  * callbacks (array) change

  * renderfunction (string)

  * popout (array) type/icon_class

  * export (array) xlsx/image

# Database-mutating options

  * edit (array) required(regex/message)/condition/show/trigger/# type/target/query/truevalue/falsevalue

  * insert (array) required/include/noclear/onsuccessalert/onsuccessscript/#

  * delete (array) text/notids/html/confirm

  * actions (array) #

  * selectone (array) default/trigger/name

  * selectany (array) name

  * placeholder (string): only used for selectone/selectany

  * tablefunction (array) trigger/replacetext/hidecondition/text/confirm/addparam
