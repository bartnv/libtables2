# Welcome to the Libtables documentation

Libtables allows for rapid development of dynamic, interactive web- applications that leverage the power of a relational
database backend. It is aimed at developers with a firm grasp of SQL who wish to minimize the time spent on writing the
PHP and Javascript plumbing for their web-application. Its features include:

 * Live-updating tables
 * Paginated, sortable and filterable tables
 * Inline editing of table-cells (edit-in-place)
 * Validated input forms inserting into multiple tables at once with foreign keys
 * Pulldown-menus based on 1-to-many relationships with option to add entries
 * Cell tooltips based on hidden columns
 * Custom table layouts

All client-server interaction is AJAX-based, so libtables2 is suitable to use in single-page, load-once web-applications.

## Requirements

 * PHP 5.3 or newer
 * jQuery 1 or 2
 * A PostgreSQL, MySQL or SQLite database
