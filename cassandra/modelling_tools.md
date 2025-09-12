Modelling Tools


https://dba.stackexchange.com/questions/316332/are-there-data-modelling-tools-available-for-cassandra

There are several tools that help Cassandra users design and manage schema.

Hackolade is a visual data modelling software for NoSQL and other multi-model databases. It comes with an out-of-the-box plugin that allows you to connect to Apache Cassandra and DataStax Enterprise (DSE) clusters.
DataStax DevCenter is a visual IDE for Apache Cassandra. It allows users to manage schema, build and execute CQL queries, and view results in tabular form. Features include CQL syntax highlighting and CQL command auto-completion. It is free to download from the DataStax Downloads site.
DataStax Studio is a notebook-style visual tool for CQL, Spark SQL and DSE Graph. Users can build and run CQL queries against DSE clusters and Astra DB. Users can also perform Gremlin graph traversals, and write/test/run Spark SQL queries against DSE clusters.
Noting here that Kashliev Data Modeler (KDM) is an automated data modeling tool for Apache Cassandra which allowed users to easily browse a cluster's schema. However, KDM doesn't appear to be available anymore and the website appears to have been taken down.
Keep an eye on the Ecosystem page at the official Apache Cassandra website and Anant Corporation's cassandra.tools for the curated list of tools.

