# Performance Schema metadata\_locks Table

{% hint style="info" %}
The `metadata_locks` table is available from MariaDB 10.5.2.
{% endhint %}

The `metadata_locks` table contains [metadata lock](../../../sql-statements/transactions/metadata-locking.md) information.

To enable metadata lock instrumention, at runtime:

```sql
UPDATE performance_schema.setup_instruments SET enabled='YES', timed='YES' 
  WHERE name LIKE 'wait/lock/metadata%';
```

Or in the [configuration file](../../../../server-management/install-and-upgrade-mariadb/configuring-mariadb/configuring-mariadb-with-option-files.md):

```ini
performance-schema-instrument='wait/lock/metadata/sql/mdl=ON'
```

The table is by default autosized, but the size can be configured with the [performance\_schema\_max\_metadata\_locks](../performance-schema-system-variables.md#performance_schema_max_metadata_locks) system variable.

The table is read-only, and [TRUNCATE TABLE](../../../sql-statements/table-statements/truncate-table.md) cannot be used to empty the table.

The table contains the following columns:

| Field                   | Type                | Null | Default | Description                                                                                                                                                                                                                                                                                                                                      |
| ----------------------- | ------------------- | ---- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| OBJECT\_TYPE            | varchar(64)         | NO   | NULL    | Object type. One of BACKUP, COMMIT, EVENT, FUNCTION, GLOBAL, LOCKING SERVICE, PROCEDURE, SCHEMA, TABLE, TABLESPACE, TRIGGER (unused) or USER LEVEL LOCK.                                                                                                                                                                                         |
| OBJECT\_SCHEMA          | varchar(64)         | YES  | NULL    | Object schema.                                                                                                                                                                                                                                                                                                                                   |
| OBJECT\_NAME            | varchar(64)         | YES  | NULL    | Object name.                                                                                                                                                                                                                                                                                                                                     |
| OBJECT\_INSTANCE\_BEGIN | bigint(20) unsigned | NO   | NULL    | Address in memory of the instrumented object.                                                                                                                                                                                                                                                                                                    |
| LOCK\_TYPE              | varchar(32)         | NO   | NULL    | Lock type. One of BACKUP\_FTWRL1, BACKUP\_START, BACKUP\_TRANS\_DML, EXCLUSIVE, INTENTION\_EXCLUSIVE, SHARED, SHARED\_HIGH\_PRIO, SHARED\_NO\_READ\_WRITE, SHARED\_NO\_WRITE, SHARED\_READ, SHARED\_UPGRADABLE or SHARED\_WRITE.                                                                                                                 |
| LOCK\_DURATION          | varchar(32)         | NO   | NULL    | Lock duration. One of EXPLICIT (locks released by explicit action, for example a global lock acquired with [FLUSH TABLES WITH READ LOCK](../../../sql-statements/administrative-sql-statements/flush-commands/flush.md)) , STATEMENT (locks implicitly released at statement end) or TRANSACTION (locks implicitly released at transaction end). |
| LOCK\_STATUS            | varchar(32)         | NO   | NULL    | Lock status. One of GRANTED, KILLED, PENDING, POST\_RELEASE\_NOTIFY, PRE\_ACQUIRE\_NOTIFY, TIMEOUT or VICTIM.                                                                                                                                                                                                                                    |
| SOURCE                  | varchar(64)         | YES  | NULL    | Source file containing the instrumented code that produced the event, as well as the line number where the instrumentation occurred. This allows one to examine the source code involved.                                                                                                                                                        |
| OWNER\_THREAD\_ID       | bigint(20) unsigned | YES  | NULL    | Thread that requested the lock.                                                                                                                                                                                                                                                                                                                  |
| OWNER\_EVENT\_ID        | bigint(20) unsigned | YES  | NULL    | Event that requested the lock.                                                                                                                                                                                                                                                                                                                   |

<sub>_This page is licensed: CC BY-SA / Gnu FDL_</sub>

{% @marketo/form formId="4316" %}
