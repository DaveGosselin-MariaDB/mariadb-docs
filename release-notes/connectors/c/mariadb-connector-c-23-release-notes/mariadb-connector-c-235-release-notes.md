# Connector/C 2.3.5 Release Notes

The most recent [_**Stable**_](../../../community-server/about/release-criteria.md) _**(GA)**_ release of MariaDB Connector/C is:[**MariaDB Connector/C 3.4.5**](../mariadb-connector-c-3-4-release-notes/mariadb-connector-c-3-4-5-release-notes.md)

[Download](https://downloads.mariadb.org/connector-c/2.3.5)[Release Notes](mariadb-connector-c-235-release-notes.md)[Changelog](../changelogs/mariadb-connector-c-23-changelogs/mariadb-connector-c-235-changelog.md)[About MariaDB Connector/C](https://github.com/mariadb-corporation/docs-release-notes/blob/test/en/about-mariadb-connector-c/README.md)

**Release date:** 18 Jan 2018

This is a [_**Stable**_](../../../community-server/about/release-criteria.md) _**(GA)**_ release of the MariaDB\
Connector/C, formerly known as MariaDB Client Library for C.

**For a description of this library see the**[**MariaDB Connector/C**](https://app.gitbook.com/s/CjGYMsT2MVP4nd3IyW2L/mariadb-connector-c) **page.**

## Notable Bug Fixes

* [CONC-292](https://jira.mariadb.org/browse/CONC-292): Fixed malloc result check in dynamic columns
* [MDEV-10361](https://jira.mariadb.org/browse/MDEV-10361): Don't try to reconnect twice in mysql\_ping
* [CONC-301](https://jira.mariadb.org/browse/CONC-301): In case of a truncation the statement status was not updated correctly and further calls to mysql\_stmt\_fetch\_column failed

## New features/functionality

* New Debian installation layout (cmake option -DINSTALL\_LAYOUT=DEB)
* [CONC-299](https://jira.mariadb.org/browse/CONC-299): Add support for new utf8mb4 collations

For a list of changes made in this release, with links to detailed\
information on each push, see the[changelog](../changelogs/mariadb-connector-c-23-changelogs/mariadb-connector-c-235-changelog.md).

{% include "../../../.gitbook/includes/announce.md" %}

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/7hzG0V6AUK8DqF4oiVaW/" %}

{% @marketo/form formid="4316" formId="4316" %}
