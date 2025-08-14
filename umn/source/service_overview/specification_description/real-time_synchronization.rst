:original_name: drs_01_0314.html

.. _drs_01_0314:

Real-Time Synchronization
=========================

Precautions
-----------

The performance indicators provided in this section are for reference only. The actual environment is affected by factors such as the performance of the source or destination database, network bandwidth, data model, and service model.

Specifications
--------------

.. table:: **Table 1** Full synchronization maximum performance

   +--------------------------+-----------------------------------------------------------------------+
   | Data Flow                | Reference Value of Maximum Performance of Full Synchronization (MB/s) |
   +==========================+=======================================================================+
   | MySQL as the source      | 50                                                                    |
   +--------------------------+-----------------------------------------------------------------------+
   | Oracle as the source     | 40                                                                    |
   +--------------------------+-----------------------------------------------------------------------+
   | Redis as the source      | 30                                                                    |
   +--------------------------+-----------------------------------------------------------------------+
   | GaussDB as the source    | 40                                                                    |
   +--------------------------+-----------------------------------------------------------------------+
   | PostgreSQL as the source | 30                                                                    |
   +--------------------------+-----------------------------------------------------------------------+
   | DDM as the source        | 20                                                                    |
   +--------------------------+-----------------------------------------------------------------------+
   | MongoDB as the source    | 20                                                                    |
   +--------------------------+-----------------------------------------------------------------------+

.. caution::

   -  There are many factors that affect the DRS migration speed. The current migration speed is the test data when **there is no network and database performance bottlenecks and the task specifications are large**. The migration speed is for reference only.
   -  When the destination database is Oracle, the migration speed in the full phase is 30% to 50% lower than that of other types of databases due to the write mechanism of the destination database.
   -  The write performance of the MongoDB database is affected by the number of indexes. The write performance decreases by 5% to 8% when there is one index. The more indexes, the slower the write speed.

Based on the incremental performance of data flow types, there are six types of specifications: micro, small, medium, large, ultra-large, and macro. :ref:`Table 2 <drs_01_0314__en-us_topic_0000001205627773_table85411966426>` lists the performance upper limit of each specification.

.. _drs_01_0314__en-us_topic_0000001205627773_table85411966426:

.. table:: **Table 2** Performance upper limit

   +----------------+-------------------------------------------------------------------------------------+
   | Specifications | Reference Value of Maximum Performance of Incremental Synchronization (Rows/Second) |
   +================+=====================================================================================+
   | Micro          | 300                                                                                 |
   +----------------+-------------------------------------------------------------------------------------+
   | Small          | 3,000                                                                               |
   +----------------+-------------------------------------------------------------------------------------+
   | Medium         | 7,500                                                                               |
   +----------------+-------------------------------------------------------------------------------------+
   | Large          | 10,000                                                                              |
   +----------------+-------------------------------------------------------------------------------------+
   | Ultra-large    | 20,000                                                                              |
   +----------------+-------------------------------------------------------------------------------------+
   | Macro          | > 20,000                                                                            |
   +----------------+-------------------------------------------------------------------------------------+

.. note::

   -  The performance of each specification is affected by factors such as the networks, source and destination database performance, and latency. The values in the table are for reference only.
   -  DRS measures the performance of different specifications using the full (with flow control disabled) and incremental synchronization tasks as the standard.
   -  The maximum performance (rows/second) is measured by the number of transactions synchronized per second. The statement types include BEGIN, COMMIT, DML (INSERT, DELETE, and UPDATE), and DDL.
   -  If you want to compare values for a DRS task, select large or higher specifications when creating the DRS task.

Testing Models
--------------

Create a full+incremental real-time synchronization task for two RDS for MySQL instances. :ref:`Table 3 <drs_01_0314__en-us_topic_0000001205627773_table4847105511912>` shows the instance configurations.

.. _drs_01_0314__en-us_topic_0000001205627773_table4847105511912:

.. table:: **Table 3** Instance specifications

   +-------------------------+------------------------------------+------------------------------------+
   | Parameter               | Source RDS for MySQL instance      | Destination RDS for MySQL instance |
   +=========================+====================================+====================================+
   | Flavor                  | c6.4xlarge.4 (general-enhanced II) | c6.4xlarge.4 (general-enhanced II) |
   +-------------------------+------------------------------------+------------------------------------+
   | Instance specifications | Ultra-high I/O                     | Ultra-high I/O                     |
   +-------------------------+------------------------------------+------------------------------------+
   | Storage type            | 16 vCPUs|64 GB                     | 16 vCPUs|64 GB                     |
   +-------------------------+------------------------------------+------------------------------------+
   | Storage space           | 300 GB                             | 300 GB                             |
   +-------------------------+------------------------------------+------------------------------------+
   | Maximum connections     | 18,000                             | 18,000                             |
   +-------------------------+------------------------------------+------------------------------------+
   | Maximum QPS             | 3,325                              | 3,325                              |
   +-------------------------+------------------------------------+------------------------------------+
   | Maximum IOPS            | 114,152                            | 114,152                            |
   +-------------------------+------------------------------------+------------------------------------+

Test model:

-  The number of test tables is 20.
-  All test tables have primary keys.
-  The record size is 1 KB.
-  Each transaction contains two DML operations and one COMMIT operation. The ratio of INSERT, UPDATE, and DELETE operations is 1:1:1.
