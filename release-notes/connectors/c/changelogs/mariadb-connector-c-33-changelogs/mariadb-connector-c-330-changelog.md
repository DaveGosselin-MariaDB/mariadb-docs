# Connector/C 3.3.0 Changelog

The most recent [_**Stable**_](../../../../community-server/about/release-criteria.md) _**(GA)**_ release of MariaDB Connector/C is:[**MariaDB Connector/C 3.4.5**](../../mariadb-connector-c-3-4-release-notes/mariadb-connector-c-3-4-5-release-notes.md)

[Download](https://mariadb.com/downloads/#connectors)[Release Notes](../../mariadb-connector-c-33-release-notes/mariadb-connector-c-330-release-notes.md)[Changelog](mariadb-connector-c-330-changelog.md)[About MariaDB Connector/C](https://github.com/mariadb-corporation/docs-release-notes/blob/test/en/about-mariadb-connector-c/README.md)

**Release date:** 15 Feb 2022

For the highlights of this release, see the[release notes](../../mariadb-connector-c-33-release-notes/mariadb-connector-c-330-release-notes.md).

The revision number links will take you to the revision's page on GitHub. On[GitHub](https://github.com/MariaDB/mariadb-connector-c/) you can view more\
details of the revision and view diffs of the code modified in that revision.

* [Revision #340f920](https://github.com/mariadb-corporation/mariadb-connector-c/commit/340f920)\
  2022-02-10 15:08:59 +0100
  * Fix for static windows library (mariadbclient):
* [Revision #39d1913](https://github.com/mariadb-corporation/mariadb-connector-c/commit/39d1913)\
  2022-02-04 17:30:01 +0100
  * older zstd doesn't have ZSTD\_CLEVEL\_DEFAULT
* [Revision #378f787](https://github.com/mariadb-corporation/mariadb-connector-c/commit/378f787)\
  2022-02-04 16:14:03 +0100
  * don't add ZSTD\_INCLUDE\_DIRS to include dirs if no zstd
* [Revision #840136f](https://github.com/mariadb-corporation/mariadb-connector-c/commit/840136f)\
  2022-02-04 15:03:58 +0100
  * allow zstd to be disabled
* [Revision #21b91cc](https://github.com/mariadb-corporation/mariadb-connector-c/commit/21b91cc)\
  2022-02-04 15:14:00 +0100
  * removed aurora plugin from CMakeLists.txt
* [Revision #77d2585](https://github.com/mariadb-corporation/mariadb-connector-c/commit/77d2585)\
  2022-02-04 15:04:54 +0100
  * Merge branch '3.2' into 3.3
* [Revision #c08063a](https://github.com/mariadb-corporation/mariadb-connector-c/commit/c08063a)\
  2022-02-04 14:53:42 +0100
  * Removed bundled ZStandard compression library.
* [Revision #d04c5d3](https://github.com/mariadb-corporation/mariadb-connector-c/commit/d04c5d3)\
  2022-01-31 17:49:37 +0100
  * Fix zlib and zstd static build
* [Revision #e2bbe58](https://github.com/mariadb-corporation/mariadb-connector-c/commit/e2bbe58)\
  2022-01-31 15:59:04 +0100
  * removed redundant closing curly brace
* [Revision #59a5d53](https://github.com/mariadb-corporation/mariadb-connector-c/commit/59a5d53)\
  2022-01-28 06:11:13 +0100
  * zstd build fixes:
* [Revision #53c8c1c](https://github.com/mariadb-corporation/mariadb-connector-c/commit/53c8c1c)\
  2022-01-26 19:47:53 +0100
  * Set package suffix to rc1
* [Revision #2ffe908](https://github.com/mariadb-corporation/mariadb-connector-c/commit/2ffe908)\
  2022-01-26 19:41:32 +0100
  * Windows build fix
* [Revision #f3c036e](https://github.com/mariadb-corporation/mariadb-connector-c/commit/f3c036e)\
  2022-01-26 09:03:31 +0100
  * Merge branch '3.2' into 3.3
* [Revision #72fe313](https://github.com/mariadb-corporation/mariadb-connector-c/commit/72fe313)\
  2022-01-25 06:42:37 +0100
  * Travis fixes:
* [Revision #770cf22](https://github.com/mariadb-corporation/mariadb-connector-c/commit/770cf22)\
  2022-01-25 05:02:33 +0100
  * [CONC-575](https://jira.mariadb.org/browse/CONC-575): Support for MySQL zstd compression
* [Revision #b5c1a23](https://github.com/mariadb-corporation/mariadb-connector-c/commit/b5c1a23)\
  2022-01-25 03:52:42 +0100
  * Merge branch '3.2' into 3.3
* [Revision #493dce6](https://github.com/mariadb-corporation/mariadb-connector-c/commit/493dce6)\
  2022-01-23 21:00:01 +0100
  * Merge pull request #156 from devnexen/dflybsd\_build\_fix
* [Revision #58d33ed](https://github.com/mariadb-corporation/mariadb-connector-c/commit/58d33ed)\
  2021-02-24 20:17:22 +0000
  * config binary path: dragonflybsd build little update
* [Revision #721a41d](https://github.com/mariadb-corporation/mariadb-connector-c/commit/721a41d)\
  2022-01-14 20:10:05 +0100
  * Merge branch '3.2' into 3.3
* [Revision #ddb031b](https://github.com/mariadb-corporation/mariadb-connector-c/commit/ddb031b)\
  2022-01-07 17:54:25 +0100
  * Travis fix:
* [Revision #141fb0d](https://github.com/mariadb-corporation/mariadb-connector-c/commit/141fb0d)\
  2022-01-04 10:37:12 +0100
  * Test fixes:
* [Revision #dae2d11](https://github.com/mariadb-corporation/mariadb-connector-c/commit/dae2d11)\
  2022-01-03 06:34:59 +0100
  * Windows build fixes
* [Revision #510c7e5](https://github.com/mariadb-corporation/mariadb-connector-c/commit/510c7e5)\
  2022-01-02 14:14:39 +0100
  * New options MARIADB\_CONNECTION\_BYTES\_READ/SENT
* [Revision #bc7bbd4](https://github.com/mariadb-corporation/mariadb-connector-c/commit/bc7bbd4)\
  2021-12-31 17:20:46 +0100
  * Merge branch '3.2' into 3.3
* [Revision #0489f34](https://github.com/mariadb-corporation/mariadb-connector-c/commit/0489f34)\
  2021-12-22 07:18:27 +0100
  * Merge branch '3.2' into 3.3
* [Revision #7c29edf](https://github.com/mariadb-corporation/mariadb-connector-c/commit/7c29edf)\
  2021-11-21 15:18:17 +0100
  * Follow up of merge from Sutou Kouhei:
* [Revision #a4f40a3](https://github.com/mariadb-corporation/mariadb-connector-c/commit/a4f40a3)\
  2021-11-21 15:17:41 +0100
  * Merge branch '3.2' into 3.3
* [Revision #37b3760](https://github.com/mariadb-corporation/mariadb-connector-c/commit/37b3760)\
  2021-11-18 17:00:45 +0100
  * travis:
* [Revision #a1feead](https://github.com/mariadb-corporation/mariadb-connector-c/commit/a1feead)\
  2021-11-11 19:08:43 +0100
  * [CONC-365](https://jira.mariadb.org/browse/CONC-365): Failover capabilities
* [Revision #515361d](https://github.com/mariadb-corporation/mariadb-connector-c/commit/515361d)\
  2021-11-05 06:31:58 +0100
  * [CONC-274](https://jira.mariadb.org/browse/CONC-274): connection string support
* [Revision #159219f](https://github.com/mariadb-corporation/mariadb-connector-c/commit/159219f)\
  2021-11-03 16:36:48 +0100
  * Merge branch '3.2' into 3.3
* [Revision #9c64567](https://github.com/mariadb-corporation/mariadb-connector-c/commit/9c64567)\
  2021-10-11 17:55:43 +0200
  * Move new members of rpl\_event structure to the end.
* [Revision #e8fc259](https://github.com/mariadb-corporation/mariadb-connector-c/commit/e8fc259)\
  2021-10-09 10:44:04 +0200
  * [CONC-467](https://jira.mariadb.org/browse/CONC-467): Rotate event doesn't handle filename correctly
* [Revision #004f9d4](https://github.com/mariadb-corporation/mariadb-connector-c/commit/004f9d4)\
  2021-10-09 08:26:15 +0200
  * [CONC-470](https://jira.mariadb.org/browse/CONC-470): Support for semi synchronous replication
* [Revision #52934a1](https://github.com/mariadb-corporation/mariadb-connector-c/commit/52934a1)\
  2021-10-08 10:26:06 +0200
  * Merge branch '3.2' into 3.3
* [Revision #e142c3b](https://github.com/mariadb-corporation/mariadb-connector-c/commit/e142c3b)\
  2021-09-14 07:11:19 +0200
  * Skip test for [CONC-544](https://jira.mariadb.org/browse/CONC-544) when testing against SkySQL/MaxScale.
* [Revision #7e0be5a](https://github.com/mariadb-corporation/mariadb-connector-c/commit/7e0be5a)\
  2021-09-14 06:24:56 +0200
  * [CONC-544](https://jira.mariadb.org/browse/CONC-544): restrict authentication plugins
* [Revision #fc9bfcd](https://github.com/mariadb-corporation/mariadb-connector-c/commit/fc9bfcd)\
  2021-09-14 06:21:18 +0200
  * bump version numer to 3.3.0

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/7hzG0V6AUK8DqF4oiVaW/" %}

{% @marketo/form formid="4316" formId="4316" %}
