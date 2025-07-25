# Connector/J 1.1.4 Release Notes

{% include "../../../.gitbook/includes/latest-java.md" %}

**Release date:** 10 Sept 2013

MariaDB Java Client 1.1.4 is a [_**Stable**_](../../../community-server/about/release-criteria.md) _**(GA)**_\
release. In general this means that there are no known serious bugs,\
except for those marked as feature requests, that no bugs were fixed\
since last release that caused a notable code changes, and that we\
believe the code is ready for general usage (based on bug inflow).

**For a description of the MariaDB Java Client see the**[**About the MariaDB Java Client**](https://github.com/mariadb-corporation/docs-release-notes/blob/test/kb/en/about-the-mariadb-java-client/README.md) **page.**

For a list of all changes made in this release, with links to detailed\
information on each push, see the[changelog](../changelogs/1.1/mariadb-java-client-114-changelog.md).

## New functionality

It is now possible to connect to the server via Unix domain sockets (on Unix\
platforms) or shared memory (Windows). For domain socket connections, add\
"`localSocket=<socket_path>`" to the connection URL. For shared memory\
connections, add "`sharedMemory=<shared_memory_base_name>`".

Shared memory and unix domain socket support is implemented using Java Native\
Access (JNA) library, and this means that applications that use these features\
will need jna.jar and jna-platform.jar to be present in the classpath at\
runtime ([CONJ-50](https://jira.mariadb.org/browse/CONJ-50), [CONJ-51](https://jira.mariadb.org/browse/CONJ-51)). More information about the JNA project can be found\
at [jna](https://github.com/twall/jna)

## Bugs fixed in this release

Some of the bugs fixed include:

* `ResultSet.getTimestamp()` did not work with TIME columns ([CONJ-54](https://jira.mariadb.org/browse/CONJ-54))
* `DatabaseMetaData` will now return correct information about case\
  senstivity handling, dependent on `lower_case_table_names` database\
  parameter([CONJ-55](https://jira.mariadb.org/browse/CONJ-55))
  * `supportsMixedCaseIdentifiers(),supportsMixedCaseQuotedIdentifiers()`\
    will return true if `lower_case_table_names` is 0 (case-sensitive)
  * `storesLowerCaseIdentifiers(),storesLowerCaseQuotedIdentifiers()` will\
    return true if `lower_case_table_names` is 1 ( case-insensitive, lowercase\
    conversion)
  * `storesMixedCase[Identifiers(),storesMixedCaseQuotedIdentifiers()` will\
    returns true if `lower_case_table_names` is 2 (case-insensitive, but\
    case-preserving)
* `DatabaseMetaData.getDatabaseMinorVersion()` incorrectly returned major\
  version instead of minor ([CONJ-56](https://jira.mariadb.org/browse/CONJ-56))
* `PreparedStatement.setObject()` now correctly handles objects of\
  type `java.util.Date` ([CONJ-57](https://jira.mariadb.org/browse/CONJ-57))
* If connection is idle, `Statement.cancel()` is now a no-op. Previously,\
  "KILL QUERY" was sent to database no matter whether statement was executed or\
  not ([CONJ-58](https://jira.mariadb.org/browse/CONJ-58))
* Provide public method `Driver.unloadDriver()` to cleanup after driver\
  unload, to workaround Tomcat's classloading issues ([CONJ-61](https://jira.mariadb.org/browse/CONJ-61))
* Make `PreparedStatement.toString()` output more meaningful ([CONJ-62](https://jira.mariadb.org/browse/CONJ-62))

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/pNHZQXPP5OEz2TgvhFva/" %}

{% @marketo/form formid="4316" formId="4316" %}
