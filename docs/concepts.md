# Libtables concepts

## Minimize boilerplate PHP/HTML code

Libtables was initially created to avoid the repetitiveness of formatting tabular data with
HTML table elements by hand. Further on, other functionality such as edit-in-place and
insert mechanics were added. Libtables allows you to describe the elements and functionality
the tables need to have, rather than spell them out for each item individually. In other words,
Libtables is more of a declarative way to create web-tables than an imperative way.

## Harness the strengths of SQL

Where possible, Libtables allows you to use the strengths of SQL, as opposed to many
ORMs which completely abstract the SQL away. In most Libtables functions you can use
the full power of the SQL language. As such it is expected that you do type-conversions
and string concatenations in the SQL queries, rather than afterwards using PHP.

The drawback of this approach is that switching a Libtables application from one database
type to another may take more time to deal with differences in SQL dialects.

## Hashtags and column numbers

Each query to populate a Libtables table needs to start with the unique "id" column for
that table. This column is not shown to the user but is used internally all the time. We
count columns starting from zero, so column 0 is the id number and column 1 is the first
column visible to the user.

Most Libtables function parameters that allow text inputs will interpret hashtags inside
these strings. The basic hashtags are column numbers such as "#0", "#1", "#2" etc to use
the values of each row in texts that relate to that row. For instance the 'appendcell'
option commonly uses #0 to construct a URL with an id number inside it.

## Blocks

The main organizing unit in Libtables is the block. A block can contain any HTML
and/or PHP, but generally it will contain one or more lt_* functions. Blocks need
to be separate files because they have to be loaded both from regular pageviews
as well as AJAX-calls to Libtables' data.php. The latter is done so that the server
can verify whether certain operations are allowed.

You can use global PHP variables like $_SESSION in blocks, but only the ones that
are always available, regardless of the request method. $_GET is not available for
the AJAX requests, so it can't be used inside blocks.

Blocks are included in the main flow of your website by calling lt_print_block().
This function can be used recursively, so a block can include another block. Some
libtables workflows operate by replacing the content of the current block with that
of another block.

## Parameters

Each Libtables block can have parameters passed into it by using the lt_print_block()
function. These parameters are used within your application to keep track of things like
'the logged in user' or 'the currently selected product'. Block parameters can be used
in all SQL queries by using the questionmark symbol for parameter substitution. Within
the PHP you can use the $params array, so $params[0] is the first parameter and $params[1]
the second.

Block parameters normally are set from $_SESSION variables or from incoming $_GET or $_POST
parameters.
