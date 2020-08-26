# edit
  * edit (array): allow in-cell editing of the specified columns

Basic example:
```php
  'edit' => [
    3 => 'user.firstname',
    4 => 'user.lastname'
  ]
```

  * edit (array): all options
    * target (string): the column to store the entered data in &lt;table>.&lt;column> format
    * type (string): change the type of the used input element; available options are:
        * multiline: use a &lt;textarea> element allowing line-breaks in the input
        * checkbox: use a &lt;input type="checkbox"> element; also allows the use of the 'truevalue' and 'falsevalue' suboptions to change the way boolean values are interpreted
          from and written to the database
        * date: use a &lt;input type="date"> element which presents a native date-picker UI in supporting browsers; falls back to normal text input otherwise
        * password: use a &lt;input type="password"> element which masks out the input
        * email: use a &lt;input type="email"> element which enforces a valid email address as input in supporting browsers; falls back to normal text input otherwise
        * color: use a color picker as input element; requires https://github.com/mrgrain/colpick to be loaded. Saves the color's #-code in the cell
        * number: use a &lt;input type="number"> element which presents up/down arrows in supporting browsers; falls back to normal text input otherwise. Also allows the use of
          'min' and 'max' suboptions that set limits on the permitted input
        * datauri: use a file upload element; the uploaded file should be an image and will be stored in the database as a data uri (to be used in conjunction with [transformations -> image](https://bart.noordervliet.net/lt-docs/table_options_display/#transformations-experimental))
          note: there is currently no size limit and automatic resizing is not yet implemented, so beware of bloating your database with giant files
    * query (string): query to generate a pulldown menu from; should produce a foreign key and a description.
      The foreign key is stored in the 'target' column, the description is shown in the user interface.
    * required (boolean or array): enforce that the field cannot be left empty
        * regex (string): only accept input matching this regular expression
        * message (string): show this message if the input is invalid
    * condition (array): sets a condition that must be true for the field to be editable; needs to have 3 elements in the array, the left-hand side, the comparison type
      (either '==' or '!=') as a string and the right-hand side. The left-hand side will expand hash-tags like '#2' meaning 'the value of column 2 in this row'.
    * show (string): [experimental] only supports the value 'always' currently, which makes the edit input always visible, not just after clicking
    * trigger (string): refresh the indicated other table whenever this table is changed through edit; needs to contain the 'tag' name of the other table
    * idcolumn (integer): normally, the row and table to edit are defined by the first column in the select query containing the id of the row to update after an edit; if the cell to be updated is in an other table, the idcolumn makes it possible to specify the row and table that has to be updated

Full example:
```php
  'edit' => [
    1 => 'table.column1',
    2 => [ 'target' => 'table.column2', 'type' => 'multiline' ],
    3 => [ 'target' => 'table.column3', 'type' => 'checkbox', 'truevalue' => 't', 'falsevalue' => 'f' ],
    4 => [ 'target' => 'table.column4', 'type' => 'number', 'min' => 1, 'max' => 100 ],
    5 => [ 'target' => 'table.column9', 'type' => 'datauri' ],
    6 => [ 'target' => 'table.column5', 'query' => 'SELECT id, description FROM othertable' ],
    7 => [ 'target' => 'table.column6', 'required' => true ],
    8 => [ 'target' => 'table.column7', 'required' => [ 'regex' => '\d{4}', 'message' => 'Input is not a 4-digit code' ] ],
    9 => [ 'target' => 'table.column8', 'condition' => [ '#3', '==', 't' ] ],
    10 => [ 'target' => 'othertable.column2', 'idcolumn' => 4 ]
    'trigger' => 'tag'
  ]
```

# insert
  * insert (array): add a row to the table to insert new data

Basic example:
```php
  'insert' => [
    3 => 'user.firstname',
    4 => 'user.lastname'
  ]
```

  * insert (array): it is common to allow insertion of all columns that are already configured for 'edit'; this can be done with the 'include' suboption. The example below
    includes the 'edit' configuration and adds column 5 purely for the insert function.

Include example:
```php
  'insert' => [
    'include' => 'edit',
    5 => [ 'table.column5' ]
  ]
```

  * insert (array): all options
    * target (string): the column to store the entered data in &lt;table>.&lt;column> format
    * type (string): change the type of the used input element; available options are:
        * multiline: use a &lt;textarea> element allowing line-breaks in the input
        * checkbox: use a &lt;input type="checkbox"> element; also allows the use of the 'truevalue' and 'falsevalue' suboptions to change the way boolean values are interpreted
          from and written to the database
        * date: use a &lt;input type="date"> element which presents a native date-picker UI in supporting browsers; falls back to normal text input otherwise
        * password: use a &lt;input type="password"> element which masks out the input
        * email: use a &lt;input type="email"> element which enforces a valid email address as input in supporting browsers; falls back to normal text input otherwise
        * color: use a color picker as input element; requires https://github.com/mrgrain/colpick to be loaded. Saves the color's #-code in the cell
        * number: use a &lt;input type="number"> element which presents up/down arrows in supporting browsers; falls back to normal text input otherwise. Also allows the use of
          'min' and 'max' suboptions that set limits on the permitted input
    * query (string): query to generate a pulldown menu from; should produce a foreign key and a description.
      The foreign key is stored in the 'target' column, the description is shown in the user interface.
    * required (boolean or array): enforce that the field cannot be left empty
        * regex (string): only accept input matching this regular expression
        * message (string): show this message if the input is invalid
    * default (string): default value to put in the input element when it is created or emptied
    * placeholder (string): html5 placeholder attribute to set on the input element; shown whenever the input element is empty
    * submit (string): label to be used as a text on the insert button
    * class (string): CSS class name to set on the input element, in addition to the default ones
    * trigger (string): refresh the indicated other table whenever this table is changed through edit; needs to contain the 'tag' name of the other table
    * next (string): when the insert button is clicked, replace this block with the block named in this option; the new block is invoked with the id of the
      newly inserted entry as its first parameter (use it as $params[0] from PHP)
    * include (string): input definitions to reuse; currently only supports 'edit' to use the edit-definitions
    * noclear (boolean): if set to true, the insert input fields are not cleared after each insert is done
    * onsuccessalert (string): text to show in a javascript alert() after the insert was done succesfully
    * onsuccessscript (string): code to be evaluated in a javascript eval() after the insert was done succesfully
    * hidden (array): hidden data to insert alongside the user-entered fields (may also be an array of arrays to insert multiple hidden fields)
        * target (string): the column to store the hidden data in &lt;table>.&lt;column> format
        * value (string): the value to store; this is commonly a PHP-variable

Full example:
```php
  'insert' => [
    1 => 'table.column1',
    2 => [ 'target' => 'table.column2', 'type' => 'multiline' ],
    3 => [ 'target' => 'table.column3', 'type' => 'checkbox', 'truevalue' => 't', 'falsevalue' => 'f' ],
    4 => [ 'target' => 'table.column4', 'type' => 'number', 'min' => 1, 'max' => 100 ],
    5 => [ 'target' => 'table.column5', 'query' => 'SELECT id, description FROM othertable' ],
    6 => [ 'target' => 'table.column6', 'required' => true ],
    7 => [ 'target' => 'table.column7', 'required' => [ 'regex' => '\d{4}', 'message' => 'Input is not a 4-digit code' ] ],
    'trigger' => 'tag',
    'noclear' => true,
    'onsuccessalert' => 'Row inserted succesfully',
    'onsuccessscript' => "$('#status').addClass('status-ok')",
    'hidden' => [
      'target' => 'table.userid',
      'value' => $_SESSION['userid']
    ]
  ]
```

# delete
  * delete (array): render a row-delete button at the end of each row

Basic example:
```php
  'delete' => [
    'table' => 'user',
    'text' => 'Delete user',
    'confirm' => 'Are you sure you want to delete user with ID #0?'
  ]
```

  * delete (array): all options
    * text (string): text to use on the button instead of the Unicode cross-symbol (✖)
    * html (string): html to use instead of the &lt;input type="button"> element; will be wrapped with an &lt;a> element to handle the onclick
    * confirm (string): text to show in a javascript confirm() dialog to request confirmation from the user; hashtags in this string are interpreted
    * notids (array): id-numbers of rows that may not be deleted
    * update (array): instead of an SQL DELETE statement, run an UPDATE with the data specified in the 'column' and 'value' suboptions
        * column (array): the column to change in the UPDATE
        * value (string): the value to write to the column

Full example:
```php
  'delete' => [
    'table' => 'user',
    'html' => '<img src="delete.svg">',
    'notids' => [ $_SESSION['userid'] ],
    'update' => [
      'column' => 'active'
      'value' => 'false'
    ]
  ]
```

# selectone [experimental]
  * selectone (array): render radiobuttons to select one row in the table, to be used from javascript elsewhere in the page
    * name (string): name used for button column in the table header
    * default (string): specify which row should be selected before user interaction; currently either 'first' or 'last'
    * trigger: ?
```php
  'selectone' => [
    'name' => 'Select',
    'default' => 'first'
  ]
```

# selectany [experimental]
  * selectany (array): render checkboxes to select multiple rows in the table; this is saved to the specified linktable (many-to-many relationship) using the
    first parameter of this block (the first field in 'fields') and the id of the row (the second field in 'fields')
    * name (string): name used for the checkbox column in the table header
    * linktable (string): SQL table name of the linktable
    * fields (array of strings): the two column names for the foreign keys going into the linktable
    * id (integer): the id to use for the first foreign key instead of the first block parameter which is the default
```php
  'selectany' => [
    'name' => 'Select',
    'linktable' => 'user_groups',
    'fields' => [ 'user_id', 'group_id'],
    'id' => $_SESSION['userid']
  ]
```

# placeholder [experimental]
  * placeholder (string): disabled default option in the pulldown menu for render mode 'select'


# actions [experimental]
  * actions (array of arrays): render button(s) at the end of each row to run a custom query or load a certain block
    * name (string): descriptive text for the function to be used on the button; hashtags in this string are interpreted
    * condition (string): comparison to be evaluated in a javascript eval(); if the comparison is false, the action button is not shown for that row;
      hashtags in this string are interpreted
    * confirm (string): text to show in a javascript confirm() dialog to request confirmation from the user before running the action; hashtags in this string are interpreted
    * query (string): query to run on the database when the action button is clicked; hashtags in this string are interpreted
    * block (string): block to load (replacing the current one) when the action button is clicked
    * params (array): only used with the 'block' option above; specifies the parameters to use with the new block; hashtags are interpreted
```php
  'actions' => [
    [ 'name' => 'Mark paid', 'query' => 'UPDATE payment SET paid = true WHERE id = #0', 'condition' => '"#2" == "no"' ],
    [ 'name' => 'Go to order', 'block' => 'show-order', 'params' => [ '#0' ], 'condition' => '"#2" == "yes"' ]
  ]
```


# tablefunction [experimental]
  * tablefunction (array): render an action button at the top of the table running a function for the table as a whole
    * text (string, required): text to be printed on the action button
    * replacetext (string): text to be printed on the action button after the first succesful use
    * confirm (string): text to show in a javascript confirm() dialog to request confirmation from the user; hashtags in this string are interpreted
    * hidecondition (string): SQL query to determine whether or not to show the button; re-run on every refresh of the table; the output is boolean-evaluated in javascript
    * query (string): SQL query to run when the button is clicked
    * trigger (string): refresh the indicated other table whenever this function has run; needs to contain the 'tag' name of the other table
    * addparam (array): request an additional parameter from the user to be appended to the parameters for the query
      text (string, required): text to show the user in the parameter dialog
```php
  'tablefunction' => [
    'text' => 'Confirm',
    'confirm' => 'Are you sure you want to confirm all the new entries?',
    'query' => 'UPDATE table SET confirmed = true WHERE confirmed = false AND user = ' . $_SESSION['userid'],
    'hidecondition' => 'SELECT COUNT(*) = 0 FROM table WHERE confirmed = false AND user = ' . $_SESSION['userid'],
    'replacetext' => 'Confirmed'
  ]
```
