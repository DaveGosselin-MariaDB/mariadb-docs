# Connector/J 2.7.0 Changelog

{% include "../../../../.gitbook/includes/latest-java.md" %}

[Download](https://mariadb.com/downloads/#connectors)[Release Notes](../../2.7/mariadb-connector-j-270-release-notes.md)[Changelog](mariadb-connector-j-270-changelog.md)[Connector/J Overview](https://github.com/mariadb-corporation/docs-release-notes/blob/test/kb/en/about-mariadb-connector-j/README.md)

**Release date:** 25 Sep 2020

For the highlights of this release, see the[release notes](../../2.7/mariadb-connector-j-270-release-notes.md).

The revision number links will take you to the revision's page on GitHub. On[GitHub](https://github.com/MariaDB/mariadb-connector-j) you can view more\
details of the revision and view diffs of the code modified in that revision.

* [Revision #550a8ed5](https://github.com/mariadb-corporation/mariadb-connector-j/commit/550a8ed5) - Merge branch 'release/2.7.0'
* [Revision #ca8365ab](https://github.com/mariadb-corporation/mariadb-connector-j/commit/ca8365ab) - bump 2.7.0 version
* [Revision #143e8c92](https://github.com/mariadb-corporation/mariadb-connector-j/commit/143e8c92) - \[[CONJ-810](https://jira.mariadb.org/browse/CONJ-810)] normalization of resultset getDate/getTime of timestamp field.
* [Revision #8e82bc5f](https://github.com/mariadb-corporation/mariadb-connector-j/commit/8e82bc5f) - Merge branch 'develop' of [mariadb-connector-j](https://github.com/mariadb-corporation/mariadb-connector-j) into develop
* [Revision #e5f34055](https://github.com/mariadb-corporation/mariadb-connector-j/commit/e5f34055) - \[[CONJ-827](https://jira.mariadb.org/browse/CONJ-827)] update maxscale test to recent version
* [Revision #5bf84cca](https://github.com/mariadb-corporation/mariadb-connector-j/commit/5bf84cca) - \[[CONJ-827](https://jira.mariadb.org/browse/CONJ-827)] update maxscale test to recent version
* [Revision #8e2d523d](https://github.com/mariadb-corporation/mariadb-connector-j/commit/8e2d523d) - \[[CONJ-830](https://jira.mariadb.org/browse/CONJ-830)] issue SSL negotiation only if server show SSL capability. The connector was initiating SSL negotiation when option `useSsl` is set even if server doesn't support SSL. This was resulting throwing a wrong exception that doesn't show the initial problem
* [Revision #4f798679](https://github.com/mariadb-corporation/mariadb-connector-j/commit/4f798679) - \[[CONJ-829](https://jira.mariadb.org/browse/CONJ-829)] Option to cache callablestatement disabled by default
* [Revision #49f14d63](https://github.com/mariadb-corporation/mariadb-connector-j/commit/49f14d63) - \[misc] skysql test suite correction
* [Revision #6601971b](https://github.com/mariadb-corporation/mariadb-connector-j/commit/6601971b) - \[[CONJ-828](https://jira.mariadb.org/browse/CONJ-828)] new option `ensureSocketState`
* [Revision #6f02333e](https://github.com/mariadb-corporation/mariadb-connector-j/commit/6f02333e) - Merge branch 'pull/156' into develop
* [Revision #0e8d5739](https://github.com/mariadb-corporation/mariadb-connector-j/commit/0e8d5739) - \[[CONJ-805](https://jira.mariadb.org/browse/CONJ-805)] maxFieldSize truncation correction #156
* [Revision #a8f9b5fc](https://github.com/mariadb-corporation/mariadb-connector-j/commit/a8f9b5fc) - \[[CONJ-817](https://jira.mariadb.org/browse/CONJ-817)] correction handling default data when resultset is using binary protocol
* [Revision #79a9b64b](https://github.com/mariadb-corporation/mariadb-connector-j/commit/79a9b64b) - \[[CONJ-825](https://jira.mariadb.org/browse/CONJ-825)] XAResource.isSameRM test correction
* [Revision #eebe1e58](https://github.com/mariadb-corporation/mariadb-connector-j/commit/eebe1e58) - \[misc] test update for local infile and 10.5 server
* [Revision #41d39b6c](https://github.com/mariadb-corporation/mariadb-connector-j/commit/41d39b6c) - \[[CONJ-817](https://jira.mariadb.org/browse/CONJ-817)] Table with primary key with DEFAULT function can not be inserted to: Current position is after the last row. correction for 10.5 server
* [Revision #70c406b2](https://github.com/mariadb-corporation/mariadb-connector-j/commit/70c406b2) - \[[CONJ-825](https://jira.mariadb.org/browse/CONJ-825)] XAResource.isSameRM did always return false
* [Revision #a49abc13](https://github.com/mariadb-corporation/mariadb-connector-j/commit/a49abc13) - \[misc] travis test [MariaDB 10.5](../../../../community-server/old-releases/mariadb-10-5-series/what-is-mariadb-105.md) addition
* [Revision #09541596](https://github.com/mariadb-corporation/mariadb-connector-j/commit/09541596) - \[[CONJ-812](https://jira.mariadb.org/browse/CONJ-812)] DatabaseMetadata getBestRowIdentifier pseudo code correction for server without IS\_GENERATED column in INFORMATION\_SCHEMA.COLUMNS
* [Revision #f3055c7c](https://github.com/mariadb-corporation/mariadb-connector-j/commit/f3055c7c) - \[[CONJ-812](https://jira.mariadb.org/browse/CONJ-812)] DatabaseMetadata getBestRowIdentifier and getMaxProcedureNameLength correction
* [Revision #7363e257](https://github.com/mariadb-corporation/mariadb-connector-j/commit/7363e257) - \[[CONJ-814](https://jira.mariadb.org/browse/CONJ-814)] DatabaseMetadata result-set PK\_NAME now contains value
* [Revision #ed706d53](https://github.com/mariadb-corporation/mariadb-connector-j/commit/ed706d53) - \[[CONJ-816](https://jira.mariadb.org/browse/CONJ-816)] correct test using default UUID() to supported version
* [Revision #47d01e79](https://github.com/mariadb-corporation/mariadb-connector-j/commit/47d01e79) - \[misc] update appveyor server version to latest
* [Revision #5a20980d](https://github.com/mariadb-corporation/mariadb-connector-j/commit/5a20980d) - \[[CONJ-820](https://jira.mariadb.org/browse/CONJ-820)] test correction when using prepare
* [Revision #a0b65b87](https://github.com/mariadb-corporation/mariadb-connector-j/commit/a0b65b87) - \[[CONJ-817](https://jira.mariadb.org/browse/CONJ-817)] ResultSet.insertRow improvement for default value handling - detailed error when inserting data with empty primary key for server before 10.4 - permits insert for empty primary key with default value for 10.5 server (value is retrieved using RETURNING)
* [Revision #3c8452e7](https://github.com/mariadb-corporation/mariadb-connector-j/commit/3c8452e7) - \[[CONJ-817](https://jira.mariadb.org/browse/CONJ-817)] DatabaseMetadata.getProcedures REMARKS and PROCEDURE\_TYPE ordering correction
* [Revision #87bf787d](https://github.com/mariadb-corporation/mariadb-connector-j/commit/87bf787d) - \[[CONJ-820](https://jira.mariadb.org/browse/CONJ-820)] PreparedStatement.setObject doesn't support java.lang.Character type
* [Revision #5340e647](https://github.com/mariadb-corporation/mariadb-connector-j/commit/5340e647) - Merge branch 'pull/159' into develop
* [Revision #25cae561](https://github.com/mariadb-corporation/mariadb-connector-j/commit/25cae561) - \[misc] suppress warning
* [Revision #e00a351d](https://github.com/mariadb-corporation/mariadb-connector-j/commit/e00a351d) - \[misc] SkySQL testing
* [Revision #a88d392f](https://github.com/mariadb-corporation/mariadb-connector-j/commit/a88d392f) - Merge branch 'pull/157' into develop
* [Revision #88189ffc](https://github.com/mariadb-corporation/mariadb-connector-j/commit/88189ffc) - \[[CONJ-805](https://jira.mariadb.org/browse/CONJ-805)] fix StringIndexOutOfBoundsException for >1 byte UTF8 characters and maxFieldSize set
* [Revision #e7628511](https://github.com/mariadb-corporation/mariadb-connector-j/commit/e7628511) - for-[CONJ-742](https://jira.mariadb.org/browse/CONJ-742)-and-[CONJ-807](https://jira.mariadb.org/browse/CONJ-807), add Driver.class.getClassLoader() can solve squirrel problem. But static introduce access denied
* [Revision #f2cfbaa6](https://github.com/mariadb-corporation/mariadb-connector-j/commit/f2cfbaa6) - Fix - setConfiguration not being called on classes that extend ConfigurableSocketFactory
* [Revision #a5c414d3](https://github.com/mariadb-corporation/mariadb-connector-j/commit/a5c414d3) - \[misc] setting good travis link
* [Revision #6f101ce3](https://github.com/mariadb-corporation/mariadb-connector-j/commit/6f101ce3) - Merge tag '2.6.2' into develop
* [Revision #c290bfef](https://github.com/mariadb-corporation/mariadb-connector-j/commit/c290bfef) - Reproduce issue with polish chars and set maxFieldSize

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/pNHZQXPP5OEz2TgvhFva/" %}

{% @marketo/form formid="4316" formId="4316" %}
