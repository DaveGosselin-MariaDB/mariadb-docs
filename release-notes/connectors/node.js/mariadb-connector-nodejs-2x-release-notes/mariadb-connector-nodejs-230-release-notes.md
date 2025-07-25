# Connector/Node.js 2.3.0 Release Notes

{% include "../../../.gitbook/includes/latest-nodejs.md" %}

[Download](https://mariadb.com/downloads/#connectors) | [Release Notes](mariadb-connector-nodejs-230-release-notes.md) | [Changelog](../changelogs/mariadb-connector-nodejs-2x-changelogs/mariadb-connector-nodejs-230-changelog.md) | [Connector/Node.js Overview](https://app.gitbook.com/s/CjGYMsT2MVP4nd3IyW2L/mariadb-connector-nodejs/mariadb-connector-node-js-guide)

**Release date:** 20 Mar 2020

MariaDB Connector/Node.js 2.3.0 is a [_**Stable**_](../../../community-server/about/release-criteria.md) _**(GA)**_ release.

{% hint style="success" %}
**For an overview of MariaDB Connector/Node.js see the** [**About MariaDB Connector/Node.js**](https://app.gitbook.com/s/CjGYMsT2MVP4nd3IyW2L/mariadb-connector-nodejs/mariadb-connector-node-js-guide) **page**
{% endhint %}

2.3.0 has been deprecated to 2.3.1: changing new connection option `timeout` to `queryTimeout` to avoid any confusion.

* [CONJS-127](https://jira.mariadb.org/browse/CONJS-127) - Resultset with same identifier skip data. Now an error will be thrown.
* [CONJS-126](https://jira.mariadb.org/browse/CONJS-126) - permit setting session query timeout per option
* [CONJS-124](https://jira.mariadb.org/browse/CONJS-124) - Force connection.escapeId to emit backtick #101
* [CONJS-123](https://jira.mariadb.org/browse/CONJS-123) - exporting SqlError class to permit instanceOf checks #100
* [CONJS-122](https://jira.mariadb.org/browse/CONJS-122) - fix undefined localTz with timezone: 'Z' issue #92
* [CONJS-121](https://jira.mariadb.org/browse/CONJS-121) - Connection.escapeId must always quote value to permit reserved words

misc:

* appveyor testing server version upgrade
* better debug logging trace format
* correct ssl test

## Changelog

For a complete list of changes made in this release, with links to detailed information\
on each push, see the [changelog](../changelogs/mariadb-connector-nodejs-2x-changelogs/mariadb-connector-nodejs-230-changelog.md).

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/pNHZQXPP5OEz2TgvhFva/" %}

{% @marketo/form formid="4316" formId="4316" %}
