:original_name: drs_14_0003.html

.. _drs_14_0003:

How Do I Configure the Shard Key for a MongoDB Sharded Cluster?
===============================================================

MongoDB shards data at the collection level, distributing the collection data using shard keys.

You choose the shard key when sharding a collection. Each record contains a shard key, and the shard key is either an indexed field or indexed compound fields. MongoDB database distributes data in different chunks according to the shard key, and distributes chunks evenly among the shards. To divide data chunks by shard key, MongoDB database uses two sharding methods: range-based sharding and hashed sharding.

.. table:: **Table 1** Shard key classification

   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Shard Key Type        | Description                                                                                                                                                                                                                | Application Scenario                                                                                                                                             |
   +=======================+============================================================================================================================================================================================================================+==================================================================================================================================================================+
   | Range-based sharding  | Ranged-based sharding involves dividing data into contiguous ranges determined by the shard key values. Range-based sharding is the default sharding methodology if no other options are specified.                        | It is recommended when the shard key has high cardinality with low frequency, and the shard key value does not change monotonically.                             |
   |                       |                                                                                                                                                                                                                            |                                                                                                                                                                  |
   |                       | This allows for efficient queries where reads target documents within a contiguous range. The distribution route determines which data chunk stores the data required and forwards the request to the corresponding shard. |                                                                                                                                                                  |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Hashed sharding       | Hashed sharding uses a hashed index to partition data across your shared cluster and to create chunks.                                                                                                                     | If the shard key values that have a high cardinality or change monotonically, or there are large number of different values, hashed sharding is an ideal option. |
   |                       |                                                                                                                                                                                                                            |                                                                                                                                                                  |
   |                       | Hashed sharding provides more even data distribution across the sharded cluster Hash values enable data to be randomly distributed in each chunk, and therefore are randomly distributed in different shards.              |                                                                                                                                                                  |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Once you shard a collection, the shard key and the shard key values are immutable. If you need to modify the shard key of a document, you must delete the document. Then modify the shard key and insert the document again.

.. note::

   The shard key does not support array indexes, text indexes, geographical indexes, and spatial indexes.

Range-based Sharding
--------------------

#. Run the following command to enable database sharding:

   **sh.enableSharding**\ *(database)*

   .. note::

      **database** indicates the database for which the sharded collection is enabled.

#. Configure the collection's shard key.

   **sh.shardCollection**\ *(namespace, key)*

   .. note::

      -  **namespace** consists of a string <database>.<collections> specifying the full namespace of the target collection.
      -  **key** indicates the index for the shard key.

   -  If the collection is empty, skip this step because the index on the shard key can be created automatically.

      **sh.shardCollection()**

   -  If the collection is not empty, create an index key. Then, run the following command to set the shard key:

      **sh.shardCollection()**

Hashed Sharding
---------------

#. Run the following command to enable database sharding:

   **sh.enableSharding**\ *(database)*

   .. note::

      **database** indicates the database for which the sharded collection is enabled.

#. Set hashed shard keys.

   **sh.shardCollection**\ (*"<database>.<collection>", { <shard key> : "hashed" }* , false, {numInitialChunks: *Number of preconfigured chunks*})

   The value of **numInitialChunks** is calculated as follows: db.collection.stats().size / 10*1024*1024*1024.

   If the collection contains data, run the following command to create a hashed index for the hashed key:

   **db.collection.createIndex()**

   Run the following command to create a hashed shard key:

   **sh.shardCollection()**
