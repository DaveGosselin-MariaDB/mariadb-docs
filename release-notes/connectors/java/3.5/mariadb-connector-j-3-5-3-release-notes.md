# Connector/J 3.5.3 Release Notes

{% include "../../../.gitbook/includes/latest-java.md" %}

<a href="https://mariadb.com/downloads/connectors/connectors-data-access/java8-connector" class="button primary">Download</a> <a href="mariadb-connector-j-3-5-3-release-notes.md" class="button secondary">Release Notes</a> <a href="../changelogs/3.5/mariadb-connector-j-3-5-3-changelog.md" class="button secondary">Changelog</a> <a href="https://app.gitbook.com/s/CjGYMsT2MVP4nd3IyW2L/mariadb-connector-j/about-mariadb-connector-j" class="button secondary">Connector/J Overview</a>

**Release date:** 27 Mar 2025

MariaDB Connector/J 3.5.3 is a [_**Stable**_](../../../community-server/about/release-criteria.md) _**(GA)**_ release.

{% hint style="info" %}
**For an overview of MariaDB Connector/J see the** [**About MariaDB Connector/J**](https://app.gitbook.com/s/CjGYMsT2MVP4nd3IyW2L/mariadb-connector-j/about-mariadb-connector-j) **page**
{% endhint %}

## Notable Changes

* Resolved timestamp string representation incompatibility between versions 2.7 and 3.x ([CONJ-1232](https://jira.mariadb.org/browse/CONJ-1232))\
  Added new option [oldModeNoPrecisionTimestamp](https://app.gitbook.com/s/CjGYMsT2MVP4nd3IyW2L/mariadb-connector-j/about-mariadb-connector-j#oldmodenoprecisiontimestamp)
* Modified redirection option to enable by default only when SSL is enabled ([CONJ-1235](https://jira.mariadb.org/browse/CONJ-1235))

## Bugs Fixed

### Date and Time Handling

* Fixed issue where dates containing zero day or month resulted in a DateTimeException ([CONJ-1226](https://jira.mariadb.org/browse/CONJ-1226))

### Result Set and Metadata

* Fixed incorrect values returned by ResultSet.getColumnType() for unsigned values ([CONJ-1222](https://jira.mariadb.org/browse/CONJ-1222))
* Corrected regression in 3.x affecting column metadata for unsigned types ([CONJ-1241](https://jira.mariadb.org/browse/CONJ-1241))
* Fixed CallableStatement.getParameterMetadata() returning wrong java.sql.Type for boolean values ([CONJ-1243](https://jira.mariadb.org/browse/CONJ-1243))

### Connection Management

* Prevented NPE (Null Pointer Exception) after reconnection failure in high availability configurations ([CONJ-1236](https://jira.mariadb.org/browse/CONJ-1236))
* Fixed issue with incorrect statements.isClosed value after closing connection ([CONJ-1237](https://jira.mariadb.org/browse/CONJ-1237))

### Protocol and Performance

* Disabled BULK operations when no parameters are present ([CONJ-1239](https://jira.mariadb.org/browse/CONJ-1239))
* Fixed connectivity issues with databases that only accept TLSv1.3 ([CONJ-1240](https://jira.mariadb.org/browse/CONJ-1240))

## Changelog

For a complete list of changes made in MariaDB Connector/J 3.5.3, with links to detailed\
information on each push, see the [changelog](../changelogs/3.5/mariadb-connector-j-3-5-3-changelog.md).

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/pNHZQXPP5OEz2TgvhFva/" %}

{% @marketo/form formid="4316" formId="4316" %}
