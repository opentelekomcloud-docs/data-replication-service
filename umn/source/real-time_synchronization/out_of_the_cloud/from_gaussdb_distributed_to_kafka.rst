:original_name: drs_11_0454.html

.. _drs_11_0454:

From GaussDB Distributed to Kafka
=================================

Supported Source and Destination Databases
------------------------------------------

.. table:: **Table 1** Supported databases

   +-----------------------------------+-----------------------------------+
   | Source DB                         | Destination DB                    |
   +===================================+===================================+
   | -  GaussDB Distributed            | -  Kafka                          |
   |                                   |                                   |
   |                                   |    0.11 or later                  |
   +-----------------------------------+-----------------------------------+

Supported Synchronization Objects
---------------------------------

:ref:`Table 2 <drs_11_0454__table1051911613257>` lists the objects that can be synchronized in different scenarios. DRS will automatically check the objects you selected before the synchronization.

.. _drs_11_0454__table1051911613257:

.. table:: **Table 2** Supported synchronization objects

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Synchronization Scope                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   +===================================+=====================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | Synchronization scope             | -  Instance-level synchronization is not supported. Only one database can be synchronized at a time. To synchronize multiple databases, create multiple tasks.                                                                                                                                                                                                                                                                                                      |
   |                                   | -  **Supported scenario:** Incremental synchronization                                                                                                                                                                                                                                                                                                                                                                                                              |
   |                                   | -  **Supported fields:** INTEGER, TINYINT, SMALLINT, BIGINT, NUMBER, NUMERIC, REAL, DOUBLE PRECISION, CHARACTER, CHARACTER VARYING, NVARCHAR2, BIT, BIT VARYING, BLOB, BYTEA, CLOB, RAW, TEXT, JSON, BOOLEAN, DATE, SMALLDATETIME, TIME WITH TIME ZONE, TIME WITHOUT TIME ZONE, TIMESTAMP WITH TIME ZONE, TIMESTAMP WITHOUT TIME ZONE, INTERVAL, BOX, CIDR, CIRCLE, INET, LSEG, MACADDR, MONEY, PATH, POINT, POLYGON, TSQUERY, TSVECTOR, REFCURSOR, UUID and ARRAY. |
   |                                   | -  Table-level synchronization or object file import is supported.                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                                   |    -  Only DML statements of the selected table can be synchronized.                                                                                                                                                                                                                                                                                                                                                                                                |
   |                                   |    -  Databases without schemas cannot be synchronized.                                                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   |    -  Schemas without tables cannot be synchronized.                                                                                                                                                                                                                                                                                                                                                                                                                |
   |                                   |    -  Column-store tables, compressed tables, delay tables, and temporary tables cannot be synchronized. Do not synchronize unlogged tables.                                                                                                                                                                                                                                                                                                                        |
   |                                   |    -  The database name, schema name, and table name cannot contain special characters **/<.>\\'`|,?!**                                                                                                                                                                                                                                                                                                                                                             |
   |                                   |    -  If you select tables by importing an object file, ensure that the imported table exists in the source database or is visible to the synchronization user.                                                                                                                                                                                                                                                                                                     |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Database User Permission Requirements
-------------------------------------

Before you start a synchronization task, the source and destination database users must meet the requirements in the following table. Different types of synchronization tasks require different permissions. For details, see :ref:`Table 3 <drs_11_0454__table41931320142616>`. DRS automatically checks the database account permissions in the pre-check phase and provides handling suggestions.

.. note::

   -  You are advised to create an independent database account for DRS task connection to prevent task failures caused by account modification.
   -  After changing the account passwords for the source or destination databases, :ref:`modify the connection information <drs_10_0016>` in the DRS task as soon as possible to prevent automatic retry after a task failure. Automatic retry will lock the database accounts.

.. _drs_11_0454__table41931320142616:

.. table:: **Table 3** Database user permission

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Incremental                                                                                                                                                                                                          |
   +===================================+======================================================================================================================================================================================================================+
   | Source database user              | The user has the sysadmin role or the following minimum permissions:                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                      |
   |                                   | The REPLICATION permission or the permission inherited from the built-in role **gs_role_replication**, the CONNECT permission for databases, the USAGE permission for schemas, and the SELECT permission for tables. |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _drs_11_0454__section1113413054519:

Suggestions
-----------

-  The success of database synchronization depends on environment and manual operations. To ensure a smooth synchronization, perform a synchronization trial before you start the synchronization to help you detect and resolve problems in advance.
-  It is recommended that you start a task during off-peak hours to minimize the impact of synchronization on your services.

.. _drs_11_0454__section449714073815:

Precautions
-----------

DRS incremental synchronization consists of three phases: task start, incremental synchronization, and task completion. To ensure smooth synchronization, read the following notes before creating a synchronization task.

.. table:: **Table 4** Precautions

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Constraints                                                                                                                                                                                                                                                       |
   +===================================+===================================================================================================================================================================================================================================================================+
   | Starting a task                   | -  **Source database requirements:**                                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                                   |
   |                                   |    If incremental synchronization is selected:                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                                   |
   |                                   |    -  The **wal_level** parameter of the source database is set to **logical**.                                                                                                                                                                                   |
   |                                   |    -  The **enable_slot_log** parameter of the source database is set to **on**.                                                                                                                                                                                  |
   |                                   |    -  The **max_replication_slots** value of the source database must be greater than the number of used replication slots.                                                                                                                                       |
   |                                   |    -  Set the **REPLICA IDENTITY** attribute of a table without a primary key to **FULL**, or add a primary key to the table.                                                                                                                                     |
   |                                   |    -  Set the **REPLICA IDENTITY** attribute of the table that has a primary key to **FULL**.                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                                   |
   |                                   | -  **Source database object requirements:**                                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                                                   |
   |                                   |    -  The names of the source database, schema, and table to be synchronized cannot contain special characters **/<.>\\'`|,?!**                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                   |
   |                                   | -  **Destination database requirements:**                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                   |
   |                                   |    -  The destination database is a Kafka database.                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                   |
   |                                   | -  **Other notes:**                                                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                   |
   |                                   |    -  The source must be a distributed GaussDB instance on the current cloud.                                                                                                                                                                                     |
   |                                   |    -  Before a task enters the incremental synchronization phase, ensure that long-running transactions are not started in the source database. Starting the long transaction will block the creation of the logical replication slot and cause the task to fail. |
   |                                   |    -  If a logical replication slot fails to be created or does not exist due to a long transaction, you can reset the task and then restart it.                                                                                                                  |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Incremental synchronization       | -  Do not change the port of the source and destination databases, or change or delete the passwords and permissions of the source and destination database users. Otherwise, the task may fail.                                                                  |
   |                                   | -  Do not change the REPLICA IDENTITY value of a table in the source database. Otherwise, incremental data may be inconsistent or the task may fail.                                                                                                              |
   |                                   | -  During migration of table-level objects, you are not advised to rename the tables.                                                                                                                                                                             |
   |                                   | -  Replication of interval partition tables is not supported.                                                                                                                                                                                                     |
   |                                   | -  After a DDL statement is executed in a transaction, the DDL statement and subsequent statements are not decoded.                                                                                                                                               |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Stopping a task                   | -  **Stop a task normally:**                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                   |
   |                                   |    -  When an incremental synchronization task is complete, the streaming replication slot created by the task in the source database is automatically deleted.                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                   |
   |                                   | -  **Forcibly stop a task:**                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                   |
   |                                   |    -  To forcibly stop an incremental synchronization task, delete the replication slots that may remain in the source database. For details, see :ref:`Forcibly Stopping Synchronization from GaussDB Distributed <drs_03_1131>`.                                |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Prerequisites
-------------

-  You have logged in to the DRS console.
-  For details about the DB types and versions supported by real-time synchronization, see :ref:`Real-Time Synchronization <drs_01_0302>`.

-  You have read :ref:`Suggestions <drs_11_0454__section1113413054519>` and :ref:`Precautions <drs_11_0454__section449714073815>`.

Procedure
---------

#. On the **Data Synchronization Management** page, click **Create Synchronization Task**.

#. On the **Create Synchronization Instance** page, specify the task name, description, and the synchronization instance details, and click **Next**.

   .. table:: **Table 5** Task and recipient description

      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter   | Description                                                                                                                                      |
      +=============+==================================================================================================================================================+
      | Region      | The region where the synchronization instance is deployed. You can change the region.                                                            |
      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | Project     | The project corresponds to the current region and can be changed.                                                                                |
      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | Task Name   | The task name must start with a letter and consist of 4 to 50 characters. It can contain only letters, digits, hyphens (-), and underscores (_). |
      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description | The description consists of a maximum of 256 characters and cannot contain special characters ``!=<>'&"\``                                       |
      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

   .. table:: **Table 6** Synchronization instance settings

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                     |
      +===================================+=================================================================================================================================================+
      | Data Flow                         | Select **Out of the cloud**.                                                                                                                    |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Source DB Engine                  | Select **GaussDB Distributed**.                                                                                                                 |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Destination DB Engine             | Select **Kafka**.                                                                                                                               |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Network Type                      | The public network is used as an example. Available options: **Public network** and **VPN or Direct Connect**                                   |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Source DB Instance                | The distributed GaussDB instance you created.                                                                                                   |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Mode              | -  Incremental                                                                                                                                  |
      |                                   |                                                                                                                                                 |
      |                                   |    Through log parsing, incremental data generated on the source database is synchronized to the destination database.                          |
      |                                   |                                                                                                                                                 |
      |                                   |    During synchronization, the source database continues to provide services for external systems with zero downtime.                           |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Tags                              | -  This setting is optional. Adding tags helps you better identify and manage your tasks. Each task can have up to 20 tags.                     |
      |                                   | -  After a task is created, you can view its tag details on the **Tags** tab. For details, see :ref:`Tag Management <drs_synchronization_tag>`. |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      If a task fails to be created, DRS retains the task for three days by default. After three days, the task automatically ends.

#. On the **Configure Source and Destination Databases** page, wait until the synchronization instance is created. Then, specify source and destination database information and click **Test Connection** for both the source and destination databases to check whether they have been connected to the synchronization instance. After the connection tests are successful, click **Next**.

   Establish the connectivity between the DRS instance and the source and destination databases.

   -  **Network connectivity:** Ensure that the source and destination databases accept connections from the DRS instance.
   -  **Account connectivity:** Ensure that the source and destination databases allows connections from the DRS instance using the username and password.

   .. table:: **Table 7** Source database settings

      +-------------------+-------------------------------------------------------------------------------------------------------------------+
      | Parameter         | Description                                                                                                       |
      +===================+===================================================================================================================+
      | DB Instance Name  | The distributed GaussDB instance selected during synchronization task creation. This parameter cannot be changed. |
      +-------------------+-------------------------------------------------------------------------------------------------------------------+
      | Database Username | The username for accessing the source database.                                                                   |
      +-------------------+-------------------------------------------------------------------------------------------------------------------+
      | Database Password | The password for the database username.                                                                           |
      +-------------------+-------------------------------------------------------------------------------------------------------------------+

   .. note::

      The username and password of the source database are encrypted and stored in DRS and will be cleared after the task is deleted.

   .. table:: **Table 8** Destination database settings

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                     |
      +===================================+=================================================================================================================================================================================+
      | IP Address or Domain Name         | IP address or domain name of the destination database in the **IP address/Domain name:Port** format. The port of the destination database. Range: 1 - 65535                     |
      |                                   |                                                                                                                                                                                 |
      |                                   | You can enter up to 10 groups of IP addresses or domain names of the source database. Separate multiple values with commas (,). For example: 192.168.0.1:8080,192.168.0.2:8080. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Method                            | Available options: **PLAINTEXT**, **SSL**, **SASL_PLAINTEXT**, and **SASL_SSL**. For details, see :ref:`Kafka Authentication <drs_05_0018>`.                                    |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Set Synchronization Task** page, select the synchronization policy, objects, and data format, and click **Next**.

   .. table:: **Table 9** Synchronization Object

      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                             | Description                                                                                                                                                                                                                                                                                                       |
      +=======================================+===================================================================================================================================================================================================================================================================================================================+
      | Source Database Replication Slot Name | You can choose whether to specify the replication slot of the source database. After replication slot is enabled, enter the replication slot name. The name contains 63 characters and cannot start with a digit. Only lowercase letters, digits, and underscores (_) are allowed.                                |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Topic Synchronization Policy          | Topic synchronization policy. You can select **A specific topic** or **Auto-generated topics**.                                                                                                                                                                                                                   |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Topic                                 | Select the topic to be synchronized to the destination database. This parameter is available when the topic is set to **A specified topic**.                                                                                                                                                                      |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Topic Name Format                     | This parameter is available when **Topic Synchronization Policy** is set to **Auto-generated topics**.                                                                                                                                                                                                            |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Number of Partitions                  | This parameter is available when **Topic Synchronization Policy** is set to **Auto-generated topics**.                                                                                                                                                                                                            |
      |                                       |                                                                                                                                                                                                                                                                                                                   |
      |                                       | The number of partitions of a topic. Each topic can have multiple partitions. More partitions can provide higher throughput but consume more resources. Set the number of partitions based on the actual situation of brokers.                                                                                    |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Replication Factor                    | This parameter is available when **Topic Synchronization Policy** is set to **Auto-generated topics**.                                                                                                                                                                                                            |
      |                                       |                                                                                                                                                                                                                                                                                                                   |
      |                                       | Number of copies of a topic. Each topic can have multiple copies, and the copies are placed on different brokers in a cluster. The number of copies cannot exceed the number of brokers. Otherwise, the topic fails to be created.                                                                                |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronize Topic To                  | The policy for synchronizing topics to the Kafka partitions.                                                                                                                                                                                                                                                      |
      |                                       |                                                                                                                                                                                                                                                                                                                   |
      |                                       | -  If topics are synchronized to different partitions by hash value of the database, schema and table names, the performance on a single table query can be improved.                                                                                                                                             |
      |                                       |                                                                                                                                                                                                                                                                                                                   |
      |                                       | -  If topics are synchronized to different partitions by hash value of the primary key, one table corresponds to one topic. This prevents data from being written to the same partition, and consumers can obtain data from different partitions concurrently.                                                    |
      |                                       |                                                                                                                                                                                                                                                                                                                   |
      |                                       |    For a table without a primary key, if you select **Partitions are identified by the hash values of the primary key**, topics are synchronized to different partitions based on the hash value of the database_name.schema.table_name.                                                                          |
      |                                       |                                                                                                                                                                                                                                                                                                                   |
      |                                       | -  **Partitions are differentiated by the hash values of database_name.schema_name**: This mode applies to scenarios where one database corresponds to one topic, preventing multiple schemas from being written to the same partition, so that consumers can obtain data from different partitions concurrently. |
      |                                       |                                                                                                                                                                                                                                                                                                                   |
      |                                       | -  If topics are synchronized to partition 0, strong consistency can be obtained but write performance is impacted.                                                                                                                                                                                               |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Data Format in Kafka                  | Select the data format to be delivered to Kafka.                                                                                                                                                                                                                                                                  |
      |                                       |                                                                                                                                                                                                                                                                                                                   |
      |                                       | -  **Avro** refers to binary encoded format.                                                                                                                                                                                                                                                                      |
      |                                       | -  **JSON**: JSON message format, which is easy to interpret but takes up more space.                                                                                                                                                                                                                             |
      |                                       |                                                                                                                                                                                                                                                                                                                   |
      |                                       | For details, see :ref:`Kafka Message Format <drs_03_0052>`.                                                                                                                                                                                                                                                       |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Object                | DRS supports table-level synchronization. You can select data for synchronization based on your service requirements.                                                                                                                                                                                             |
      |                                       |                                                                                                                                                                                                                                                                                                                   |
      |                                       | .. note::                                                                                                                                                                                                                                                                                                         |
      |                                       |                                                                                                                                                                                                                                                                                                                   |
      |                                       |    -  You can search for table names to quickly select the required database objects.                                                                                                                                                                                                                             |
      |                                       |    -  If there are changes made to the source databases or objects, click in the upper right corner to update the objects to be synchronized.                                                                                                                                                                     |
      |                                       |                                                                                                                                                                                                                                                                                                                   |
      |                                       |    -  If an object name contains spaces, the spaces before and after the object name are not displayed. If there are two or more consecutive spaces in the middle of the object name, only one space is displayed.                                                                                                |
      |                                       |    -  The name of the selected synchronization object cannot contain spaces.                                                                                                                                                                                                                                      |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Check Task** page, check the synchronization task.

   -  If any check fails, review the cause and rectify the fault. After the fault is rectified, click **Check Again**.
   -  If all check items are successful, click **Next**.

      .. note::

         You can proceed to the next step only when all checks are successful. If there are any items that require confirmation, view and confirm the details first before proceeding to the next step.

#. On the **Confirm Task** page, specify **Start Time**, confirm that the configured information is correct, and click **Submit** to submit the task.

   .. table:: **Table 10** Task startup settings

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                 |
      +===================================+=============================================================================================================================================================================================+
      | Started Time                      | Set **Start Time** to **Start upon task creation** or **Start at a specified time** based on site requirements.                                                                             |
      |                                   |                                                                                                                                                                                             |
      |                                   | .. note::                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                             |
      |                                   |    After a synchronization task is started, the performance of the source and destination databases may be affected. You are advised to start a synchronization task during off-peak hours. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. After the task is submitted, you can view and manage it on the **Data Synchronization Management** page.

   -  You can view the task status. For more information about task status, see :ref:`Task Statuses <drs_06_0004>`.
   -  You can click |image1| in the upper-right corner to view the latest task status.
   -  By default, DRS retains a task in the **Configuration** state for three days. After three days, DRS automatically deletes background resources, but the task status remains unchanged. When you reconfigure the task, DRS applies for resources for the task again.

.. |image1| image:: /_static/images/en-us_image_0000001758549405.png
