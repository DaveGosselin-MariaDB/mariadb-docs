# Error 1348: Column is not updatable

| Error Code | SQLSTATE | Error                     | Description                  |
| ---------- | -------- | ------------------------- | ---------------------------- |
| 1348       | HY000    | ER\_NONUPDATEABLE\_COLUMN | Column '%s' is not updatable |

## Possible Causes and Solutions

The usual cause is that an [UPDATE](../../sql-statements/data-manipulation/changing-deleting-data/update.md), [LOAD DATA](../../sql-statements/data-manipulation/inserting-loading-data/load-data-into-tables-or-index/load-data-infile.md) or [LOAD XML](../../sql-statements/data-manipulation/inserting-loading-data/load-data-into-tables-or-index/load-xml.md), is being performed on the column of a [view](https://github.com/mariadb-corporation/docs-server/blob/test/general-resources/server-usage/views/README.md) where the view column is an expression.

<sub>_This page is licensed: CC BY-SA / Gnu FDL_</sub>

{% @marketo/form formId="4316" %}
