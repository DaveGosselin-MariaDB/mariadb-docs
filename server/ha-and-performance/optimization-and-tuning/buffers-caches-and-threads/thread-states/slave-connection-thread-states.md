# Replica Connection Thread States

This article documents thread states that are related to connection threads that occur on a replicatioin replica. These correspond to the `STATE` values listed by the [SHOW PROCESSLIST](../../../../reference/sql-statements/administrative-sql-statements/show/show-processlist.md) statement or in the [Information Schema PROCESSLIST Table](../../../../reference/system-tables/information-schema/information-schema-tables/information-schema-processlist-table.md) as well as the `PROCESSLIST_STATE` value listed in the [Performance Schema threads Table](../../../../reference/system-tables/performance-schema/performance-schema-tables/performance-schema-threads-table.md).

| Value                                     | Description                                                                                                                                               |
| ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Changing master                           | Processing a [CHANGE MASTER TO](../../../../reference/sql-statements/administrative-sql-statements/replication-statements/change-master-to.md) statement. |
| Killing slave                             | Processing a [STOP SLAVE](../../../../reference/sql-statements/administrative-sql-statements/replication-statements/stop-replica.md) statement.           |
| Opening master dump table                 | A table has been created from a master dump and is now being opened.                                                                                      |
| Reading master dump table data            | After the table created by a master dump (the Opening master dump table state) the table is now being read.                                               |
| Rebuilding the index on master dump table | After the table created by a master dump has been opened and read (the Reading master dump table data state), the index is built.                         |

<sub>_This page is licensed: CC BY-SA / Gnu FDL_</sub>

{% @marketo/form formId="4316" %}
