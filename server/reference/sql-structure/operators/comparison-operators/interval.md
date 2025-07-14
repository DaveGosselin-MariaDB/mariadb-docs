# INTERVAL

## Syntax

```
INTERVAL(N0,N1,N2,N3,...)
```

## Description

Returns the index of the last argument that is less than or equal to the first argument, or is NULL.

Returns 0 if N0 <= N1, 1 if N <= N2, 2 if N <= N3 and so on or -1 if N is NULL. All\
arguments are treated as integers. It is required that N1 <= N2 <= N3 <=\
... <= Nn for this function to work correctly because a fast binary\
search is used.

## Examples

```
SELECT INTERVAL(23, 23);
+------------------+
| INTERVAL(23, 23) |
+------------------+
|                1 |
+------------------+

SELECT INTERVAL(23, 21, 22, 23);
+--------------------------+
| INTERVAL(23, 21, 22, 23) |
+--------------------------+
|                        3 |
+--------------------------+

SELECT INTERVAL(23, 1, 15, 17, 19, 21, 23, 27, 29);
+---------------------------------------------+
| INTERVAL(23, 1, 15, 17, 19, 21, 23, 27, 29) |
+---------------------------------------------+
|                                           6 |
+---------------------------------------------+

SELECT INTERVAL(23, 1, 15, 17, 30, 44, 200);
+--------------------------------------+
| INTERVAL(23, 1, 15, 17, 30, 44, 200) |
+--------------------------------------+
|                                    3 |
+--------------------------------------+

SELECT INTERVAL(10, 1, 10, 100, 1000);
+--------------------------------+
| INTERVAL(10, 1, 10, 100, 1000) |
+--------------------------------+
|                              2 |
+--------------------------------+

SELECT INTERVAL(22, 23, 30, 44, 200);
+-------------------------------+
| INTERVAL(22, 23, 30, 44, 200) |
+-------------------------------+
|                             0 |
+-------------------------------+

SELECT INTERVAL(10, 2, NULL);
+-----------------------+
| INTERVAL(10, 2, NULL) |
+-----------------------+
|                     2 |
+-----------------------+
```

<sub>_This page is licensed: GPLv2, originally from_</sub> [<sub>_fill\_help\_tables.sql_</sub>](https://github.com/MariaDB/server/blob/main/scripts/fill_help_tables.sql)

{% @marketo/form formId="4316" %}
