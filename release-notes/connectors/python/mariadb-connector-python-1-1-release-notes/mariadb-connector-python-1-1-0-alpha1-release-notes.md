# Connector/Python 1.1.0 Alpha1 Release Notes

{% include "../../../.gitbook/includes/latest-python.md" %}

<a href="https://mariadb.com/downloads/connectors/connectors-data-access/python-connector/" class="button primary">Download</a> <a href="mariadb-connector-python-1-1-0-alpha1-release-notes.md" class="button secondary">Release Notes</a> <a href="https://app.gitbook.com/s/CjGYMsT2MVP4nd3IyW2L/connectors-quickstart-guides/connector-python-guide" class="button secondary">Connector/Python Overview</a>

**Release date:** 18 Aug 2021

This is an [_**Alpha**_](../../../community-server/about/release-criteria.md) release of MariaDB Connector/Python and not intended for production use.

{% hint style="danger" %}
**Do not use&#x20;**_**Alpha**_**&#x20;releases in production!**
{% endhint %}

**For a description of this library see the** [**MariaDB Connector/Python documentation**](https://mariadb-corporation.github.io/mariadb-connector-python/index.html)**.**

MariaDB Connector/Python enables python programs to access MariaDB and MySQL databases, using an API which is compliant with the Python DB API 2.0 (PEP-249). It is written in C and uses MariaDB Connector/C client library for client server communication.

## Notable changes

* [CONPY-97](https://jira.mariadb.org/browse/CONPY-97): All classes (including cursor and connection) are implemented in native Python. Instead of using the default cursor and connection classes, it is now possible to use own classes which are based on default classes.
* The default behaviour for cursor result sets changed: instead of using unbuffered result sets buffered result sets are used (buffered= True).
* Parser was partially reworked: Beside several fixes for different comment styles, the parser checks if binary or text protocol will be used.
* Several new constants were added. CLIENT for capability checking, FIELD\_FLAGS for use together with Cursor.descriptor, STATUS for checking current status of database server.
* For reducing releasing and locking of the GIL, executemany() method was optimized and a new method was added to MariaDB Connector/C.
* The minimum required version of Connector/C is now 3.2.4
* Documentation was updated and extended.
* New methods and attributes:
  * Connection class:
    * method begin() - starts a new transaction
    * method select\_db() - changes the default database
    * method show\_warnings() - Shows error, warning and note messages from last executed command
    * attribute client\_capabilities - allows to check the capabilities of client library
    * attribute server\_capabilities - allows to check the capabilities of connected database server
    * attribute server\_status - allows to check the current server status
    * attribute open - returns True if the connection is alive, otherwise False
  * Cursor class
    * attribute buffered - default is now True.
    * paramcount - returns the number of parameters in a statement

## Installation

MariaDB Connector/Python 1.1.0a1 can be obtained from central python repository:

```bash
pip3 install --pre mariadb
```

## Changelog

For a list of changes made in this release, with links to detailed information\
on each push, see the [changelog](../changelogs/mariadb-connector-python-11-changelogs/mariadb-connector-python-110a1-changelog.md).

## Links:

* [Documentation](https://github.com/mariadb-corporation/mariadb-connector-python/wiki)
* [Bug tracker](https://jira.mariadb.org)
* Sources are hosted on [Github](https://github.com/mariadb-corporation/mariadb-connector-python)

**Do not use&#x20;**_**alpha**_**&#x20;releases in production!**

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/pNHZQXPP5OEz2TgvhFva/" %}

{% @marketo/form formid="4316" formId="4316" %}
