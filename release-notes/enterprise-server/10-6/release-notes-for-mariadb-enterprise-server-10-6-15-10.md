# Release Notes for MariaDB Enterprise Server 10.6.15-10

MariaDB Enterprise Server 10.6.15-10 is a maintenance release of [MariaDB Enterprise Server](https://github.com/mariadb-corporation/docs-release-notes/blob/test/en/mariadb-enterprise-server/README.md) 10.6. This release includes a variety of fixes.

MariaDB Enterprise Server 10.6.15-10 was released on 2023-09-11.

## Changes in Storage Engines

* This release originally incorporated MariaDB ColumnStore engine version 23.02.4.
* This release now incorporates MariaDB ColumnStore engine version 23.10.0.

## Backports

* [JSON\_OVERLAPS()](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/sql-functions/special-functions/json-functions/json_overlaps) has been backported. (MENT-1853)
  * The `JSON_OVERLAPS()` function can be used to compare two JSON documents to determine if they have any key-value pairs or array elements in common.

```sql
SELECT JSON_OVERLAPS('{"A": 1, "B": {"C":2}}', '{"A": 2, "B": {"C":2}}') AS is_overlap;
```

```
+---------------------+
| is_overlap          |
+---------------------+
| 1                   |
+---------------------+
```

* [JSON\_SCHEMA\_VALID()](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/sql-functions/special-functions/json-functions/json_schema_valid) has been backported. (MENT-1796)
  * The `JSON_SCHEMA_VALID()` function can be used to validate a JSON document against a JSON schema, as documented by the [JSON Schema Draft 2020.](https://json-schema.org/draft/2020-12/release-notes)
  * This function can also be used in a `CHECK` constraint to verify that JSON documents are only stored in the database if they include required items and that the values are within a given range and length.

## Notable Changes

* The package for the `cracklib_password_check` plugin includes an SELinux policy, allowing the plugin to work with SELinux. ([MDEV-18374](https://jira.mariadb.org/browse/MDEV-18374))
* MariaDB Enterprise Backup reports detailed recovery progress during `mariadb-backup --prepare`. ([MDEV-29911](https://jira.mariadb.org/browse/MDEV-29911))
* With Optimizer Trace, a `sel_arg_alloc_limit_hit` record is written when `MAX_SEL_ARGS` is reached. ([MDEV-30964](https://jira.mariadb.org/browse/MDEV-30964))
  * `MAX_SEL_ARGS` is one of the limits in the optimizer that triggers short-cut of time-intensive or memory-intensive analysis for complex `WHERE` clauses.
  * For example:

```sql
SELECT
 JSON_DETAILED(JSON_EXTRACT(trace, '$**.setup_range_conditions'))
 FROM information_schema.OPTIMIZER_TRACE;
```

```json
[
   [
       {
           "sel_arg_alloc_limit_hit":
           {
              "alloced_sel_args": 16001
           }
       }
   ]
]
```

* `ANALYZE FORMAT=JSON` output includes InnoDB statistics. ([MDEV-31577](https://jira.mariadb.org/browse/MDEV-31577))
  * For example:

```json
"table": {
 "table_name": "t1",
 ...
 "r_engine_stats": {
 "pages_accessed": integer,
 "pages_updated" : integer,
 "pages_read_count" : integer,
 "pages_read_time_ms" : double_val,
 "old_rows_read" : integer,
 },
```

* Slow query log output includes InnoDB engine information. ([MDEV-31558](https://jira.mariadb.org/browse/MDEV-31558))
  * InnoDB engine information output is enabled with --log-slow-verbosity=innodb
  * Sample output:

```
# Pages_accessed: 184 Pages_read: 95 Pages_updated: 0 Undo_rows_read: 1 

# Pages_read_tim e: 17.0204 Engine_time: 248.1297

```

* Engine\_time is the time in milliseconds spent inside engine calls.
* Page\_\* variables are supported for the InnoDB storage engine.
  * For the Spider storage engine, the default values and behavior of some system variables has changed: ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
  * Prior to this release:
    * These variables used a value of -1 (the default) to indicate that Spider would use the default table value, and this value was not user visible.
    * Spider table parameters could set values, but these values would be overridden with the system variable value if the system variable was set to a value other than -1.
  * Starting with this release:
    * The default value for these system variables has been updated to reflect the actual default table value, rather than -1.
    * Where a value is set by a table parameter, this value overrides the system default and the value set by Spider system variable.
    * If a table parameter is not set, the Spider system variable's value is used. This behavior is unchanged.
  * See "Interface Changes" for a full list of updated default values.

## Issues Fixed

### Can result in data loss

* With InnoDB storage engine, when `innodb_undo_log_truncate=ON`, performing a recovery can result in a corrupted undo log. ([MDEV-31373](https://jira.mariadb.org/browse/MDEV-31373))
* With InnoDB storage engine, when database encryption is enabled only on a replica, InnoDB pages can be corrupted. ([MDEV-31347](https://jira.mariadb.org/browse/MDEV-31347), [MDEV-31156](https://jira.mariadb.org/browse/MDEV-31156))
* With InnoDB storage engine, when `innodb_undo_log_truncate=ON`, backup and recovery can fail. ([MDEV-31487](https://jira.mariadb.org/browse/MDEV-31487))
* With InnoDB storage engine, if two MariaDB Server instances using InnoDB are started with the same data directory there can be data loss. ([MDEV-31568](https://jira.mariadb.org/browse/MDEV-31568))

### Can result in a hang or crash

* With InnoDB storage engine, a hang can occur with the following error: ([MDEV-31353](https://jira.mariadb.org/browse/MDEV-31353))`[Note] InnoDB: Set innodb_force_recovery=1 to ignore corrupted pages.`
* With Aria storage engine, when Aria encryption is enabled and used but an encryption plugin is not loaded, the server can crash. ([MDEV-26258](https://jira.mariadb.org/browse/MDEV-26258))
* With Galera Cluster, a Galera node can fail while aborting a transaction. ([MDEV-30963](https://jira.mariadb.org/browse/MDEV-30963))
  * Assertion failure: `!lock.was_chosen_as_deadlock_victim`
* With Galera Cluster, when `wsrep_sst_donor` and `wsrep_cluster_address` are set to `NULL` rather than an empty string, the server can crash. ([MDEV-28433](https://jira.mariadb.org/browse/MDEV-28433))
* When accessing `information_schema.INNODB_BUFFER_PAGE` or `information_schema.INNODB_BUFFER_PAGE_LRU` after starting the server and processing a crash recovery, the server can crash. ([MDEV-31386](https://jira.mariadb.org/browse/MDEV-31386))
* When `optimizer_switch='optimize_join_buffer_size=off'` is set, the server can crash. ([MDEV-31348](https://jira.mariadb.org/browse/MDEV-31348))
* When executing a `SELECT` query using an index for `GROUP BY` and filesort, the server can crash. ([MDEV-30143](https://jira.mariadb.org/browse/MDEV-30143))
* With MariaDB Connector/C, when the `mysql_list_fields()` function is called against a view, the server can crash. ([MDEV-30159](https://jira.mariadb.org/browse/MDEV-30159))
* With Aria storage engine, changing `aria_sort_buffer_size` settings to huge numbers and executing INSERT/UPDATE can result in a crash. ([MDEV-28054](https://jira.mariadb.org/browse/MDEV-28054))
* With InnoDB storage engine, when `slave_parallel_mode` is `optimistic` and `slave_parallel_threads` is greater than 0, an `ALTER SEQUENCE` can fail with an `out-of-order` binlog error if the `SEQUENCE` uses InnoDB. ([MDEV-31503](https://jira.mariadb.org/browse/MDEV-31503))
  * Prior to this release, the following error can be raised:`Last_Error: Error 'An attempt was made to binlog GTID 0-1-100 which would create an out-of-order sequence number with existing GTID 0-1-100 and gtid stric mode is enabled' on query. Default database: 'test'. Query: 'alter sequence s1 restart with 1' will be shown.`
* With replication, when `binlog_format=ROW` is set on the primary server and `slave_run_triggers_for_rbr=1` is set on the replica server, the replica server can crash when calling a function from a different database within a TRIGGER on the replica. ([MDEV-29894](https://jira.mariadb.org/browse/MDEV-29894))
* During a simple `SELECT`, a crash can occur in `Type_handler_json_common::make_json_valid_expr` (MENT-1875)
* With `SQL_MODE=ORACLE`, a memory leak can occur on shutdown. ([MDEV-26186](https://jira.mariadb.org/browse/MDEV-26186))
* Queries in the form `SELECT DISTINCT function_returning_string(aggregate_func(...)) ... GROUP BY ...` could produce an assertion failure or wrong result. ([MDEV-31743](https://jira.mariadb.org/browse/MDEV-31743))
* With InnoDB storage engine, InnoDB can purge history too early, causing crash on undo record access in MVCC read. ([MDEV-31355](https://jira.mariadb.org/browse/MDEV-31355))
* With InnoDB storage engine, when `innodb_change_buffering=changes` and `innodb_file_per_table=0`, the server can hang. ([MDEV-31088](https://jira.mariadb.org/browse/MDEV-31088))
* With InnoDB storage engine, purge on partitioned table can lead to a crash. ([MDEV-31264](https://jira.mariadb.org/browse/MDEV-31264))
* With InnoDB storage engine, when executing a statement that rebuilds an InnoDB table (such as `TRUNCATE TABLE, OPTIMIZE TABLE, ALTER TABLE`, or as part of executing `innodb_undo_log_truncate=ON`), the server can hang. ([MDEV-31442](https://jira.mariadb.org/browse/MDEV-31442))
* With InnoDB storage engine, when a `BINARY(0)` or `VARBINARY(0)` column in an InnoDB table is indexed, the server can crash. ([MDEV-19216](https://jira.mariadb.org/browse/MDEV-19216))
* With InnoDB storage engine, when reading or writing InnoDB data pages, asynchronous I/O errors can cause the server to crash. ([MDEV-27593](https://jira.mariadb.org/browse/MDEV-27593))
* For a System Versioned table, when adding a key to a virtual column, the server can crash. ([MDEV-31416](https://jira.mariadb.org/browse/MDEV-31416))
* Setting `session_track_system_variables` globally to an invalid value can cause the server to crash. ([MDEV-25237](https://jira.mariadb.org/browse/MDEV-25237))
* With Galera Cluster, a cluster node can crash during IST when rolling back a transaction. ([MDEV-29724](https://jira.mariadb.org/browse/MDEV-29724))
* Replication from an older MariaDB Server version to a newer MariaDB Server version can break, and the server may crash. (MENT-1935)
  * A mismatch in hash values was caused by use of different hash functions, causing rows in tables having explicit or implicit unique hash indexes to be treated as different rows between different versions of MariaDB Server even though the data in the rows was the same.

### Can result in unexpected behavior

* For a System Versioned table with non-versioned columns, if the initial INSERT includes a versioned column, an "on duplicate key update" for the non-versioned column generates a history record. ([MDEV-23100](https://jira.mariadb.org/browse/MDEV-23100))
*
  * With Spider storage engine, setting a system variable overrides the value set as a table parameter. ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* With InnoDB storage engine, secondary indexes can be corrupted when a previously freed page is later reused. This is caused by change buffer entries being left behind when a page is freed. ([MDEV-31385](https://jira.mariadb.org/browse/MDEV-31385))
* The "pam\_user\_map" module does not correctly handle usernames or group names containing the "@" character. ([MDEV-31336](https://jira.mariadb.org/browse/MDEV-31336))
* With some Unicode collations, JSON functions can return incorrect results. ([MDEV-23187](https://jira.mariadb.org/browse/MDEV-23187))
* With `sql_mode=ORACLE, information_schema.ROUTINES.ROUTINE_DEFINITION` does not correctly contain the `PACKAGE` or `PACKAGE BODY` ([MDEV-30662](https://jira.mariadb.org/browse/MDEV-30662))
* Stored routines with `ROW` variables set by subselects can produce incorrect results. ([MDEV-31250](https://jira.mariadb.org/browse/MDEV-31250))
* Integer multiplication, `DIV, MOD, or ROUND/TRUNCATE` could return unexpected results when an argument is evaluated as `-9223372036854775808` ([MDEV-30932](https://jira.mariadb.org/browse/MDEV-30932))
* With Galera Cluster, when using a `KILL QUERY` statement on a Galera node that executes user transactions, GTID sequence drift can occur between writer and appliers nodes. At the same time, data consistency is maintained and `wsrep_last_committed` is in sync. ([MDEV-31075](https://jira.mariadb.org/browse/MDEV-31075))
* With Galera Cluster, creating a `TEMPORARY SEQUENCE` can cause inconsistency. ([MDEV-31335](https://jira.mariadb.org/browse/MDEV-31335))
* With Galera Cluster, the state of the cluster can only be retrieved from the primary component. ([MDEV-21479](https://jira.mariadb.org/browse/MDEV-21479))
* `information_schema.PARAMETERS` can include outdated data when a stored routine is changed in one session while the stored routine is being used in a second session. ([MDEV-31064](https://jira.mariadb.org/browse/MDEV-31064))
* Queries that use multiple `RANK` window functions can produce the wrong result. ([MDEV-20010](https://jira.mariadb.org/browse/MDEV-20010))
* Queries that use the `<` "less than" operator to compare a string with a prefixed `BLOB` key produce the wrong result. ([MDEV-31800](https://jira.mariadb.org/browse/MDEV-31800))
* Recursive CTE execution is interrupted without errors or warnings when `max_recursive_iteration`s is reached. ([MDEV-31214](https://jira.mariadb.org/browse/MDEV-31214))
  * Starting with this release, a warning occurs when `max_recursive_iterations` is reached:`Warning 1931 Query execution was interrupted. The query exceeded max_recursive_iterations = 1000. The query result may be incomplete.`
* On Microsoft Windows, when `lower_case_table_names=2`, `SHOW TABLES` does not work properly. ([MDEV-30765](https://jira.mariadb.org/browse/MDEV-30765))
* When the system is busy, `STOP REPLICA` can take a long time. ([MDEV-13915](https://jira.mariadb.org/browse/MDEV-13915))
* With parallel replication, `Seconds_Behind_Master` can show a wrong value. ([MDEV-30619](https://jira.mariadb.org/browse/MDEV-30619))
* With replication for System Versioned tables, having a parent table and a child table `WITH SYSTEM VERSIONING` where child table has a Foreign Key `CASCADE` generates orphan rows on replica. ([MDEV-31313](https://jira.mariadb.org/browse/MDEV-31313))
* With replication, when in read-only mode, `XA COMMIT/XA ROLLBACK` on the replica fails to return an error. ([MDEV-30978](https://jira.mariadb.org/browse/MDEV-30978))
* `mariadb-dump --force` can stop with the error `Couldn't execute 'SHOW CREATE FUNCTION` object`':` even though `--force` should cause the error to be ignored. ([MDEV-31092](https://jira.mariadb.org/browse/MDEV-31092))
* A query using `DISTINCT, LIMIT` with offset, and subselect to join tables produces an unexpected result. ([MDEV-28285](https://jira.mariadb.org/browse/MDEV-28285))
* The `TO_CHAR()` function returns an unclear error when an incorrect argument has been provided for the format string: ([MDEV-29152](https://jira.mariadb.org/browse/MDEV-29152))

```
ER_STD_INVALID_ARGUMENT (3047): Invalid argument error: data type of first argument must be type date/datetime/time or string in function to_char.
```

* With the ColumnStore storage engine and Federated storage engine, `ANALYZE` can return the incorrect value `0` for `r_rows` ([MDEV-29284](https://jira.mariadb.org/browse/MDEV-29284))
* With InnoDB storage engine, `SET GLOBAL innodb_undo_log_truncate=ON` does not free space when no undo logs exist. ([MDEV-31382](https://jira.mariadb.org/browse/MDEV-31382))
* With InnoDB storage engine, freed data pages are not always scrubbed. ([MDEV-31253](https://jira.mariadb.org/browse/MDEV-31253))
* With InnoDB storage engine, when setting `innodb_open_files` to a number lower than the number of tables used, an error can be shown in the server log and the operation will be aborted. ([MDEV-31256](https://jira.mariadb.org/browse/MDEV-31256))
* `ALTER TABLE .. MODIFY COLUMN` can break foreign key constraints and lead to unrestorable dumps. ([MDEV-31086](https://jira.mariadb.org/browse/MDEV-31086))
* With InnoDB storage engine, three concurrent `DELETE` by a `UNIQUE` key can cause an unexpected deadlock. ([MDEV-10962](https://jira.mariadb.org/browse/MDEV-10962))
* With InnoDB storage engine, `innochecksum` fails with `Floating point exceptio`n error. ([MDEV-31641](https://jira.mariadb.org/browse/MDEV-31641))
* With InnoDB storage engine, server status variables `Innodb_row_lock_time`, `Innodb_row_lock_time_avg` and `Innodb_row_lock_time_max` are reported in seconds instead of milliseconds. ([MDEV-29311](https://jira.mariadb.org/browse/MDEV-29311))
* With InnoDB storage engine, a duplicate entry is allowed into a UNIQUE column. ([MDEV-31120](https://jira.mariadb.org/browse/MDEV-31120))
* With InnoDB storage engine, in some rare cases InnoDB tables are being incorrectly flagged as corrupted on an I/O bound server. ([MDEV-31767](https://jira.mariadb.org/browse/MDEV-31767))
* With HashiCorp key management plugin, possible memory leaks. (MENT-1874)
* Using functions `MAX()` or `MIN()` with functions `ROUND(time)`, `CEILING(time)`, or `FLOOR(time)` as an argument can return wrong results. ([MDEV-23838](https://jira.mariadb.org/browse/MDEV-23838))
* Querying a table with a Virtual Column, when the query has a WHERE clause, can return no results. (MENT-1925)
* For transaction precise System Versioned tables, `UPDATE` can return an unexpected error: `ERROR 1761 (23000): Foreign key constraint for table 'xxx', record 'yyy' would lead to a duplicate entry in table 'xxx', key 'PRIMARY'` ([MDEV-25644](https://jira.mariadb.org/browse/MDEV-25644))
* Assertion `const_item_cache == true` failed in `Item_func::fix_fields` when a flow control statement (such as `IF())` was used in a generated column. ([MDEV-31319](https://jira.mariadb.org/browse/MDEV-31319))
* Creating a table with a foreign key (with a cascade action) defined on a base column of a virtual column is not rejected. ([MDEV-18114](https://jira.mariadb.org/browse/MDEV-18114), [MDEV-31322](https://jira.mariadb.org/browse/MDEV-31322))
  * Starting with this release, it is no longer possible to create `STORED` generated columns and `CHECK` constraints when values of the affected columns can be changed by foreign key constraint actions, such as `SET NULL` or ON `UPDATE CASCADE`.
    * Starting with this release, this results in an error like: `ERROR 1901 (HY000): Function or expression 'f_id' cannot be used in the GENERATED ALWAYS AS clause of 'v_id'`
  * Starting with this release, for existing tables with `STORED` generated columns, `SET NULL` and ON `UPDATE CASCADE` are ignored.

### Related to performance

* With InnoDB storage engine, performance regression vs MariaDB Enterprise Server 10.5 for full index scans when `innodb_flush_method=fsync` and I/O bound. (MENT-1933)
* With InnoDB storage engine, performance regression vs MariaDB Enterprise Server 10.5 for `LOAD DATA` into InnoDB tables with partitions. (MENT-1938)
* If a long-running query on one connection uses a table subject to a `ANALYZE TABLE` on another connection to collect statistics, all further queries on that table had to wait for the long-running query to finish. (MENT-1937)
* With partitioning, possible slow down of queries. ([MDEV-24712](https://jira.mariadb.org/browse/MDEV-24712))
* With InnoDB storage engine, linear read-ahead (controlled by the `innodb_read_ahead_threshold` system variable) does not work as expected. This can impact performance of `mariadb-dump` and some queries that perform a full table scan. ([MDEV-29967](https://jira.mariadb.org/browse/MDEV-29967))
* With InnoDB storage engine, query execution is slow due to incorrect estimates for range access paths. ([MDEV-30684](https://jira.mariadb.org/browse/MDEV-30684))
  * Range access paths are constructed when a query's `WHERE` clause compares indexed columns with constants.
  * Having wrong estimates can cause the optimizer to pick sub-optimal query plan, which may result in a slow query execution.

## Related to install and upgrade

* `mariadb-upgrade` can crash with `Error ""Cannot load from mysql.proc. The table is probably corrupted""` ([MDEV-28915](https://jira.mariadb.org/browse/MDEV-28915))
  * This can occur when upgrading from a release series that uses the `utf8mb3` character set for `utf8` to a release series that uses `utf8mb4` for the `utf8` character set.

## Interface Changes

* [aria\_sort\_buffer\_size](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/aria/aria-system-variables) system variable maximum value changed from `9223372036854775807` to `1152921504606846975` ([MDEV-28054](https://jira.mariadb.org/browse/MDEV-28054))
* [aria\_sort\_buffer\_size](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/aria/aria-system-variables) system variable minimum value changed from 4096 to 16376 ([MDEV-28054](https://jira.mariadb.org/browse/MDEV-28054))
* [ER\_JSON\_INVALID\_VALUE\_FOR\_KEYWORD](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/mariadb-internals/using-mariadb-with-your-programs-api/error-codes/mariadb-error-codes-4100-to-4199/e4193) error code added (MENT-1796)
* [ER\_JSON\_SCHEMA\_KEYWORD\_UNSUPPORTED](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/mariadb-internals/using-mariadb-with-your-programs-api/error-codes/mariadb-error-codes-4100-to-4199/e4194) error code added (MENT-1796)
* [ER\_QUERY\_EXCEEDED\_ROWS\_EXAMINED\_LIMIT](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/mariadb-internals/using-mariadb-with-your-programs-api/error-codes/mariadb-error-code-reference) error code removed ([MDEV-31214](https://jira.mariadb.org/browse/MDEV-31214))
* [ER\_QUERY\_RESULT\_INCOMPLETE](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/mariadb-internals/using-mariadb-with-your-programs-api/error-codes/mariadb-error-codes-1900-to-1999/e1931) error code added ([MDEV-31214](https://jira.mariadb.org/browse/MDEV-31214))
* [ER\_QUERY\_TIMEOUT](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/mariadb-internals/using-mariadb-with-your-programs-api/error-codes/mariadb-error-code-reference) error code removed
* [ER\_UNUSED\_1](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/mariadb-internals/using-mariadb-with-your-programs-api/error-codes/mariadb-error-codes-1900-to-1999/e1928) error code added
* [JSON\_OVERLAPS()](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/sql-functions/special-functions/json-functions/json_overlaps) function added (MENT-1853)
* [JSON\_SCHEMA\_VALID()](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/sql-functions/special-functions/json-functions/json_schema_valid) function added (MENT-1796)
* [myisam\_sort\_buffer\_size](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/myisam-storage-engine/myisam-system-variables) system variable maximum value changed from `18446744073709551615` to `1152921504606846975` ([MDEV-28054](https://jira.mariadb.org/browse/MDEV-28054))

## Spider Storage Engine

* [spider\_auto\_increment\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_auto_increment_mode) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_bgs\_first\_read](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_bgs_first_read) system variable default value changed from -1 to 2 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_bgs\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_bgs_mode) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_bgs\_second\_read](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_bgs_second_read) system variable default value changed from -1 to 100 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_bka\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_bka_mode) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_bka\_table\_name\_type](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_bka_table_name_type) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_buffer\_size](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_buffer_size) system variable default value changed from -1 to 16000 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_bulk\_size](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_bulk_size) system variable default value changed from -1 to 16000 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_bulk\_update\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_bulk_update_mode) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_bulk\_update\_size](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_bulk_update_size) system variable default value changed from -1 to 16000 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_casual\_read](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_casual_read) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_connect\_timeout](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_connect_timeout) system variable default value changed from -1 to 6 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_crd\_bg\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_crd_bg_mode) system variable default value changed from -1 to 2 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_crd\_interval](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_crd_interval) system variable default value changed from -1 to 51 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_crd\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_crd_mode) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_crd\_sync](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_crd_sync) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_crd\_type](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_crd_type) system variable default value changed from -1 to 2 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_crd\_weight](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_crd_weight) system variable default value changed from -1 to 2 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_delete\_all\_rows\_type](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_delete_all_rows_type) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_direct\_dup\_insert](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_direct_dup_insert) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_direct\_order\_limit](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_direct_order_limit) System Variable system variable default value changed from -1 to 9223372036854775807 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_error\_read\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_error_read_mode) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_error\_write\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_error_write_mode) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_first\_read](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_first_read) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_init\_sql\_alloc\_size](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_init_sql_alloc_size) system variable default value changed from -1 to 1024 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_internal\_limit](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_internal_limit) system variable default value changed from -1 to 9223372036854775807 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_internal\_offset](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_internal_offset) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_internal\_optimize](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_internal_optimize) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_internal\_optimize\_local](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_internal_optimize_local) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_load\_crd\_at\_startup](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_load_crd_at_startup) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_load\_sts\_at\_startup](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_load_sts_at_startup) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_low\_mem\_read](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_low_mem_read) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_max\_order](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_max_order) system variable default value changed from -1 to 32767 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_multi\_split\_read](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_multi_split_read) system variable default value changed from -1 to 100 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_net\_read\_timeout](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_net_read_timeout) system variable default value changed from -1 to 600 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_net\_write\_timeout](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_net_write_timeout) system variable default value changed from -1 to 600 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_quick\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_quick_mode) system variable default value changed from -1 to 3 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_quick\_page\_byte](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_quick_page_byte) system variable default value changed from -1 to 10485760 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_quick\_page\_size](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_quick_page_size) system variable default value changed from -1 to 1024 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_read\_only\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_read_only_mode) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_reset\_sql\_alloc](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_reset_sql_alloc) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_second\_read](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_second_read) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_select\_column\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_select_column_mode) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_selupd\_lock\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_selupd_lock_mode) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_semi\_split\_read](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_semi_split_read) system variable default value changed from -1 to 2 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_semi\_split\_read\_limit](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_semi_split_read_limit) system variable default value changed from -1 to 9223372036854775807 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_semi\_table\_lock](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_semi_table_lock) system variable default value changed from 1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_semi\_table\_lock\_connection](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_semi_table_lock_connection) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_skip\_default\_condition](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_skip_default_condition) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_skip\_parallel\_search](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_skip_parallel_search) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_split\_read](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_split_read) system variable default value changed from -1 to 9223372036854775807 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_store\_last\_crd](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_store_last_crd) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_store\_last\_sts](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_store_last_sts) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_strict\_group\_by](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_strict_group_by) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_sts\_bg\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_sts_bg_mode) system variable default value changed from -1 to 2 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_sts\_interval](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_sts_interval) system variable default value changed from -1 to 10 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_sts\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_sts_mode) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_sts\_sync](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_sts_sync) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_udf\_ct\_bulk\_insert\_interval](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_udf_ct_bulk_insert_interval) system variable default value changed from -1 to 10 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_udf\_ct\_bulk\_insert\_rows](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_udf_ct_bulk_insert_rows) system variable default value changed from -1 to 100 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_udf\_ds\_bulk\_insert\_rows](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_udf_ds_bulk_insert_rows) system variable default value changed from -1 to 3000 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_udf\_ds\_table\_loop\_mode](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_udf_ds_table_loop_mode) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_udf\_ds\_use\_real\_table](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_udf_ds_use_real_table) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_use\_handler](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_use_handler) system variable default value changed from -1 to 0 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))
* [spider\_use\_table\_charset](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-system-variables#spider_use_table_charset) system variable default value changed from -1 to 1 ([MDEV-31524](https://jira.mariadb.org/browse/MDEV-31524))

## Platforms

In alignment to the [enterprise lifecycle](../enterprise-server-lifecycle.md), MariaDB Enterprise Server 10.6.15-10 is provided for:

* CentOS 7 (x86\_64)
* Debian 10 (x86\_64, ARM64)
* Debian 11 (x86\_64, ARM64)
* Microsoft Windows (x86\_64) (MariaDB Enterprise Cluster excluded)
* Red Hat Enterprise Linux 7 (x86\_64)
* Red Hat Enterprise Linux 8 (x86\_64, ARM64)
* Red Hat Enterprise Linux 9 (x86\_64, ARM64)
* Rocky Linux 8 (x86\_64, ARM64)
* Rocky Linux 9 (x86\_64, ARM64)
* SUSE Linux Enterprise Server 12 (x86\_64)
* SUSE Linux Enterprise Server 15 (x86\_64, ARM64)
* Ubuntu 20.04 (x86\_64, ARM64)
* Ubuntu 22.04 (x86\_64, ARM64)

Some components of MariaDB Enterprise Server might not support all platforms. For additional information, see [MariaDB Corporation Engineering Policies".](https://mariadb.com/engineering-policies)

### Installation Instructions

* [MariaDB Enterprise Server ](../11-4/whats-new-in-mariadb-enterprise-server-11-4.md)[10](broken-reference)[.6](../11-4/whats-new-in-mariadb-enterprise-server-11-4.md)
* [Enterprise Cluster Topology with MariaDB Enterprise Server ](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/galera-cluster)[10](broken-reference)[.6](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/galera-cluster)
* [Primary/Replica Topology with MariaDB Enterprise Server ](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/primary-replica)[10](broken-reference)[.](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/primary-replica)[6](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/galera-cluster)
* [ColumnStore Object Storage Topology with MariaDB Enterprise Server ](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/columnstore-object-storage)[10](broken-reference)[.](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/columnstore-object-storage)[6](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/galera-cluster)[ and MariaDB Enterprise ColumnStore 23.02](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/columnstore-object-storage)
* [ColumnStore Shared Local Storage Topology with MariaDB Enterprise Server ](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/columnstore-shared-local-storage)[10](broken-reference)[.](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/columnstore-shared-local-storage)[6](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/galera-cluster)[ and MariaDB Enterprise ColumnStore 23.02](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/columnstore-shared-local-storage)
* [HTAP Topology with MariaDB Enterprise Server ](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/htap)[10](broken-reference)[.](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/htap)[6](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/galera-cluster)[ and MariaDB Enterprise ColumnStore 23.02](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/htap)
* [Single-Node Enterprise ColumnStore 23.02 with MariaDB Enterprise Server ](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/single-node-topologies/enterprise-server-with-columnstore-object-storage)[10](broken-reference)[.](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/single-node-topologies/enterprise-server-with-columnstore-object-storage)[6](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/galera-cluster)[ and Object Storage](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/single-node-topologies/enterprise-server-with-columnstore-object-storage)
* [Single-Node Enterprise ColumnStore 23.02 with MariaDB Enterprise Server ](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/single-node-topologies)[10](broken-reference)[.](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/single-node-topologies)[6](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/galera-cluster)
* [Enterprise Spider Sharded Topology with MariaDB Enterprise Server ](broken-reference)[10](broken-reference)[.](broken-reference)[6](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/galera-cluster)
* [Enterprise Spider Federated Topology with MariaDB Enterprise Server 10.](broken-reference)[6](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/architecture/topologies/galera-cluster)

## Upgrade Instructions

* [Upgrade to MariaDB Enterprise Server 10.6](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/server-management/install-and-upgrade-mariadb/upgrading/upgrading-from-to-specific-versions/upgrading-from-mariadb-10-5-to-mariadb-10-6)
* [Upgrade from MariaDB Community Server to MariaDB Enterprise Server 10.6](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/server-management/install-and-upgrade-mariadb/upgrading/upgrading-between-major-mariadb-versions)

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/pNHZQXPP5OEz2TgvhFva/" %}

{% @marketo/form formid="4316" formId="4316" %}
