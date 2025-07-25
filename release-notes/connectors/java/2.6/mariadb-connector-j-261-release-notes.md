# Connector/J 2.6.1 Release Notes

{% include "../../../.gitbook/includes/latest-java.md" %}

[Download](https://mariadb.com/downloads/#connectors)[Release Notes](mariadb-connector-j-261-release-notes.md)[Changelog](../changelogs/2.6/mariadb-connector-j-261-changelog.md)[Connector/J Overview](https://github.com/mariadb-corporation/docs-release-notes/blob/test/kb/en/about-mariadb-connector-j/README.md)

**Release date:** 23 Jun 2020

MariaDB Connector/J 2.6.1 is a [_**Stable**_](../../../community-server/about/release-criteria.md) _**(GA)**_ release.

**For an overview of MariaDB Connector/J see the**[**About MariaDB Connector/J**](https://github.com/mariadb-corporation/docs-release-notes/blob/test/kb/en/about-mariadb-connector-j/README.md) **page**

## Notable Updates

* [CONJ-781](https://jira.mariadb.org/browse/CONJ-781) - DatabaseMetaData.supportsMultipleResultSets() now return correctly true.
* [CONJ-791](https://jira.mariadb.org/browse/CONJ-791) - Using CallableStatement.getTimestamp() can't get data correctly
* [CONJ-705](https://jira.mariadb.org/browse/CONJ-705) - ParameterMetadata now return parameterCount() even if no information
* [CONJ-775](https://jira.mariadb.org/browse/CONJ-775) - avoid a NPE for malformed "jdbc:mariadb:/" connection string.
* [CONJ-776](https://jira.mariadb.org/browse/CONJ-776) - Temporal Data Tables are not listed in metadata
* [CONJ-785](https://jira.mariadb.org/browse/CONJ-785) - corrected escape sequence for multiple backslash escape
* [CONJ-786](https://jira.mariadb.org/browse/CONJ-786) - Connection.setReadOnly(true ) with option `assureReadOnly` now force read only connection even for mono server\*
* [CONJ-795](https://jira.mariadb.org/browse/CONJ-795) - permit resultset.getRow() for TYPE\_FORWARD\_ONLY when streaming
* [CONJ-797](https://jira.mariadb.org/browse/CONJ-797) - Connector set UTF8mb4 equivalent in case of server configured with UTF8mb3 collation
* [CONJ-800](https://jira.mariadb.org/browse/CONJ-800) - implement Statement setEscapeProcessing to avoid escape
* [CONJ-801](https://jira.mariadb.org/browse/CONJ-801) - possible race condition using resultset getter using label
* [CONJ-778](https://jira.mariadb.org/browse/CONJ-778) - Missing import org.osgi.service.jdbc in Import-Package clause of the OSGi manifest
* [CONJ-779](https://jira.mariadb.org/browse/CONJ-779) - Logic error in stop() method of OSGi bundle activator
* [CONJ-780](https://jira.mariadb.org/browse/CONJ-780) - Logic error in implementation of OSGi DataSourceFactory (MariaDbDataSourceFactory)
* [CONJ-788](https://jira.mariadb.org/browse/CONJ-788) - resultset metadata always indicate that column is writable even if not
* [CONJ-789](https://jira.mariadb.org/browse/CONJ-789) - ensure connection reference removal on (prepared)Statement close
* [CONJ-782](https://jira.mariadb.org/browse/CONJ-782) - SkySQL testing

## Changelog

For a complete list of changes made in MariaDB Connector/J 2.6.1, with links to detailed\
information on each push, see the [changelog](../changelogs/2.6/mariadb-connector-j-261-changelog.md).

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/pNHZQXPP5OEz2TgvhFva/" %}

{% @marketo/form formid="4316" formId="4316" %}
