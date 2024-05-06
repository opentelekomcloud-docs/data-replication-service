:original_name: drs_09_0101.html

.. _drs_09_0101:

How Do I Delete Orphaned Documents in MongoDB Sharded Clusters?
===============================================================

What Is Orphaned Document?
--------------------------

In a sharded cluster, orphaned documents are those documents on a shard that also exist in chunks on other shards as a result of failed migrations or incomplete migration cleanup due to abnormal shutdown.

Migration Impact
----------------

During cluster migration, DRS extracts full data from shards. Normal documents and orphaned documents are on different shards and DRS will migrate them all. If the conflict policy of DRS migration from MongoDB to DDS is **Ignore**, documents that are first migrated to the destination are stored, resulting in data inconsistency.

Procedure
---------

#. Contact technical support to obtain the **cleanupOrphaned** script for deleting orphaned files and decompress the script.

#. .. _drs_09_0101__en-us_topic_0000001205747809_li9814142002918:

   Modify the **cleanupOrphaned.js** script file and replace **test** with the database name of the orphaned document to be cleared.

#. .. _drs_09_0101__en-us_topic_0000001205747809_li2467154265618:

   Run the following command to clear the orphaned documents of all collections in the specified database on the shard node:

   .. code-block::

      mongo --host ShardIP --port Primaryport --authenticationDatabase database -u username -p password cleanupOrphaned.js

   .. note::

      -  **ShardIP**: indicates the IP address of the shard node.
      -  **Primaryport**: indicates the service port of the primary shard node.
      -  **database**: indicates the database name.
      -  **username**: indicates the username for logging in to the database.
      -  **password** indicates the password for logging in to the database.

   .. note::

      If you have multiple databases, repeat :ref:`2 <drs_09_0101__en-us_topic_0000001205747809_li9814142002918>` and :ref:`3 <drs_09_0101__en-us_topic_0000001205747809_li2467154265618>` to clean up orphaned documents in each database on each shard node.
