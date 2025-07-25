# Connector/C++ 1.1.1 Release Notes

The most recent [_**Stable**_](../../../community-server/about/release-criteria.md) _**(GA)**_ release of MariaDB Connector/C++ is:[**MariaDB Connector/C++ 1.1.6**](mariadb-connector-cpp-1-1-6-release-notes.md)

[MariaDB Connector/C++](https://github.com/mariadb-corporation/docs-release-notes/blob/test/en/about-mariadb-connector-cpp/README.md) is the interface between C++ applications and MariaDB Server. MariaDB Connector/C++ enables development of C++ applications using a JDBC-based API, which is also used by MariaDB Connector/J. This is the second Beta release of MariaDB Connector/C++.

MariaDB Connector/C++ 1.1.1 was released on 2022-03-04. This release is of Beta maturity, and should not be used with production workloads.

MariaDB Connector/C++ in its current implementation uses the MariaDB protocol via the MariaDB Connector/C API. Connector/C 3.3.0 is used in this release.

## Notable Changes

* MariaDB Connector/C++ 1.1.1 adds the ability to create a connection pool to improve usage of resources and to provide a faster way to connect to the server. ([CONCPP-2](https://jira.mariadb.org/browse/CONCPP-2))
  * The new class `MariaDbDataSource` has been added to enable creating a connection pool. The pool is created when `MariaDbDataSource::getConnection` is called the first time. Example:

```c++
sql::mariadb::MariaDbDataSource ds("jdbc:mariadb://localhost:3306/db?minPoolSize=2&maxPoolSize=8&maxIdleTime=900&poolValidMinDelay=2000");
ds.setUser("root");
ds.setPassword("myPassword");
// connect to server using the credentials from the pool
std::unique_ptr<sql::Connection> conn1(ds.getConnection());
std::unique_ptr<sql::Connection> conn2(ds.getConnection());
```

* Default for option `useResetConnection` has been changed from `false` to `true`. The change of default to true means the `Connection::reset()` method issues a connection reset command at the server by default. Previous default value of false meant `Connection::reset()` did a "soft reset" and set only certain system variables and connection parameters according to the connection properties.
* New connection properties have been added to configure the pool:

| Property          | Description                                                                                                                                                                                                                                                                                                                                                                                                        |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| minPoolSize       | The minimum number of connections to be kept in the pool (defaults to maxPoolSize value)                                                                                                                                                                                                                                                                                                                           |
| maxPoolSize       | The maximum number of physical connections that the pool can contain (defaults to 8)                                                                                                                                                                                                                                                                                                                               |
| maxIdleTime       | The maximum amount of time in seconds that connections above minPoolSize can stay in the pool if not used. This value must always be at least 45 seconds lower than the [@wait\_timeout](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/ha-and-performance/optimization-and-tuning/system-variables/server-system-variables#wait_timeout) value. Default: 600 in seconds(=10 minutes), minimum value is 60 seconds |
| poolValidMinDelay | The period of time in milliseconds after returning a connection to the pool, during which the connection is considered to be good and does not require validation on return to the application. 0 means validation is done each time the connection is requested (defaults to 1000)                                                                                                                                |

* New node failover support. ([CONCPP-4](https://jira.mariadb.org/browse/CONCPP-4))\
  An application can supply more than one host to use for connection. An individual port number can be specified for each host:

```c++
sql::SQLString
failoverUrl("jdbc:mariadb:sequential://localhost:3306,failoverhost1.com,[::1]:3307,failoverhost2.com:3307/db?user=root&password=someSecretWord");
std::unique_ptr<Connection> conn(DriverManager::getConnection(failoverUrl));
```

MariaDB Connector/C++ 1.1 will always try to connect to the first host in the list. Other hosts in the list will be used if a tried host cannot be reached.

* `LOAD DATA LOCAL INFILE` is not allowed by default. It can be switched on by using the `allowLocalInfile` property. ([CONCPP-93](https://jira.mariadb.org/browse/CONCPP-93)), ([CONCPP-94](https://jira.mariadb.org/browse/CONCPP-94))

## Installation

[Install MariaDB Connector/C++](https://app.gitbook.com/s/CjGYMsT2MVP4nd3IyW2L/mariadb-connector-cpp/install-mariadb-connector-cpp)

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/pNHZQXPP5OEz2TgvhFva/" %}

{% @marketo/form formid="4316" formId="4316" %}
