# Connector/C++ 1.1.2 Release Notes

The most recent [_**Stable**_](../../../community-server/about/release-criteria.md) _**(GA)**_ release of MariaDB Connector/C++ is:[**MariaDB Connector/C++ 1.1.6**](mariadb-connector-cpp-1-1-6-release-notes.md)

[MariaDB Connector/C++](https://github.com/mariadb-corporation/docs-release-notes/blob/test/en/about-mariadb-connector-cpp/README.md) is the interface between C++ applications and MariaDB Server. MariaDB Connector/C++ enables development of C++ applications using a JDBC-based API, which is also used by MariaDB Connector/J. This is the first release candidate (RC) release of MariaDB Connector/C++ 1.1.

MariaDB Connector/C++ 1.1.2 was released on 2022-11-30. This release is of Release Candidate (RC) maturity, and should not be used with production workloads.

MariaDB Connector/C++ in its current implementation uses the MariaDB protocol via the MariaDB Connector/C API. Connector/C 3.3.0 is used in this release.

## Notable Changes

* Added macOS PKG packages.
* Added support of two optimized modes of `executeBatch/executeLargeBatch` PreparedStatement methods execution: ([CONCPP-106](https://jira.mariadb.org/browse/CONCPP-106))
  * `rewriteBatchedStatements` connection option
  * `useBulkStmts` connection option

### `rewriteBatchedStatements`

* When using the `rewriteBatchedStatements` connection option, for INSERT queries the connector will construct a single query using batch parameter sets. For example:

```sql
INSERT INTO ab (i) VALUES (?) WITH first batch values = 1, second = 2
```

will be rewritten as:

```sql
INSERT INTO ab (i) VALUES (1), (2)
```

If the query cannot be rewritten in `multi-values`, the `rewriteBatchedStatements` connection option will use `multi-queries`. For example:

```sql
INSERT INTO ab(col1) VALUES (?) ON DUPLICATE KEY UPDATE col2=? WITH VALUES [1,2] AND [2,3]
```

will be rewritten as:

```sql
INSERT INTO ab(col1) VALUES (1) ON DUPLICATE KEY UPDATE col2=2;INSERT INTO TABLE(col1) VALUES (3) ON DUPLICATE KEY UPDATE col2=4
```

* If the `rewriteBatchedStatements` connection option is selected, the `useServerPrepStmts` option is set to false.
* If both `rewriteBatchedStatements` and `useBulkStmts` options are selected, `rewriteBatchedStatements` takes precedence.

### `useBulkStmts`

* The `useBulkStmts` connection option uses the MariaDB bulk execution feature, so it requires MariaDB Server 10.2.7 or later. `useBulkStmts` will be used even if `useServerPrepStmts` is not set, in other words, if the default statement prepare method is client-side prepare.
* If both `useBulkStmts` and `rewriteBatchedStatements` options are selected, `rewriteBatchedStatements` takes precedence.

## Issues Fixed

* Attempting connections from multiple threads causes the connector to crash. ([CONCPP-105](https://jira.mariadb.org/browse/CONCPP-105))
* PreparedStatement setDouble only processes the first 6 significant digits and zeros any additional digits. ([CONCPP-96](https://jira.mariadb.org/browse/CONCPP-96))
* Result-set streaming is not supported in this release series, but setting `setFetchSize` does not throw an exception and can cause the application to crash.
  * Starting with this release, setting `setFetchSize` will throw `SQLFeatureNotImplementedException` at the attempt to set `fetch size >0` ([CONCPP-107](https://jira.mariadb.org/browse/CONCPP-107))

## Installation

[Install MariaDB Connector/C++](https://app.gitbook.com/s/CjGYMsT2MVP4nd3IyW2L/mariadb-connector-cpp/install-mariadb-connector-cpp)

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/pNHZQXPP5OEz2TgvhFva/" %}

{% @marketo/form formid="4316" formId="4316" %}
