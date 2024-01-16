:original_name: drs_16_1145.html

.. _drs_16_1145:

How Does DRS Affect the Source and Destination Databases?
=========================================================

Impact on the Source
--------------------

-  During the initialization of a full migration or synchronization task, DRS needs to query all inventory data in the source database. DRS uses simple SQL statements to query data, and the query speed is limited by the I/O performance and network bandwidth of the source database. Generally, if the bandwidth is not limited, the query workload of the source database will be increased by 50 MB/s and 2 to 4 vCPUs will be occupied. If the source database is read concurrently, about 6 to 10 sessions are occupied.

   -  Fewer than eight sessions are used to query some system tables, such as tables, views, and columns in the information_schema database, in the source database.

   -  Fewer than four sessions are used to query shards in the source database. For example, in the following statement, the conditions following **select** and **where** contain only the primary key or unique key.

      .. code-block:: text

         select id from xxx where id>12345544 and limit 10000,1;

   -  Fewer than four sessions are used to query SQL statements. For example, in the following statement, the information after **select** is all column names in the table, and the condition after **where** contains only the primary key or unique key.

      .. code-block:: text

         select id,name,msg from xxx where id>12345544 and id<=12445544;

   -  The SQL statement for locking a table without a primary key is similar to the following statement. The table is locked to obtain the consistency point of the table without a primary key. After the table is locked, a connection is obtained to unlock the table.

      .. code-block:: text

         flush table xxx with read lock

      .. code-block:: text

         lock table xxx read

-  In the incremental phase, there is no pressure on the source database. Only one dump connection is available to listen to binlog incremental data in real time.

Impact on the Destination Database
----------------------------------

-  During the initialization of a full migration or synchronization task, DRS needs to write structures, inventory data, and indexes of the source database to the destination database in sequence. Generally, the total number of sessions is less than 16.

   -  Fewer than eight sessions are used to create structures.

   -  Fewer than eight sessions are writing data. Example:

      .. code-block:: text

         insert into xxx (id,name,msg) values (xxx);

   -  Fewer than eight sessions are used to create indexes. Example:

      .. code-block:: text

         alter table xxx add index xxx;

-  In the incremental phase, DRS parses the incremental data in the binlog file of the source database into SQL statements and executes the SQL statements in the destination database. Generally, the total number of sessions is less than 64.

   -  DDL statements are executed in serial mode. When a DDL statement is executed, no other DML statement is executed.
   -  There are a maximum of 64 DML connections (short connections with a timeout interval of 30 seconds). The DML statements include insert, update, delete, and replace.

.. note::

   To evaluate the impact on the source database, you can create a test task and adjust the migration policy by using rate limiting or run the test during off-peak hours.
