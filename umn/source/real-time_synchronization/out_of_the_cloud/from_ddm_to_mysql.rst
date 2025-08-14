:original_name: drs_04_0453.html

.. _drs_04_0453:

From DDM to MySQL
=================

Supported Source and Destination Databases
------------------------------------------

.. table:: **Table 1** Supported databases

   +-----------------------------------+------------------------------------+
   | Source DB                         | Destination DB                     |
   +===================================+====================================+
   | -  DDM instances                  | -  On-premises MySQL databases     |
   |                                   | -  MySQL databases on an ECS       |
   |                                   | -  MySQL databases on other clouds |
   |                                   | -  RDS for MySQL                   |
   +-----------------------------------+------------------------------------+

Prerequisites
-------------

-  You have logged in to the DRS console.
-  For details about the DB types and versions supported by real-time synchronization, see :ref:`Real-Time Synchronization <drs_01_0302>`.

Suggestions
-----------

.. caution::

   -  When a task is being started or in the full synchronization phase, do not perform DDL operations on the source database. Otherwise, the task may be abnormal.
   -  To keep data consistency before and after the synchronization, ensure that no data is written to the destination database during the synchronization.

-  The success of database synchronization depends on environment and manual operations. To ensure a smooth synchronization, perform a synchronization trial before you start the synchronization to help you detect and resolve problems in advance.

-  Start your synchronization task during off-peak hours. A less active database is easier to synchronize successfully. If the data is fairly static, there is less likely to be any severe performance impacts during the synchronization.

   -  If network bandwidth is not limited, the query rate of the source database increases by about 50 MB/s during full synchronization, and two to four CPUs are occupied.
   -  To ensure data consistency, tables to be synchronized without a primary key may be locked for 3s.
   -  The data being synchronized may be locked by other transactions for a long period of time, resulting in read timeout.
   -  When DRS concurrently reads data from a database, it will use about 6 to 10 sessions. The impact of the connections on services must be considered.
   -  If you read a table, especially a large table, during the full migration, the exclusive lock on that table may be blocked.

-  Data-Level Comparison

   To obtain accurate comparison results, start data comparison at a specified time point during off-peak hours. If it is needed, select **Start at a specified time** for **Comparison Time**. Due to slight time difference and continuous operations on data, data inconsistency may occur, reducing the reliability and validity of the comparison results.

Precautions
-----------

Before creating a synchronization task, read the following notes:

.. note::

   -  You are advised to create an independent database account for DRS task connection to prevent task failures caused by account modification.
   -  After changing the account passwords for the source or destination databases, :ref:`modify the connection information <drs_10_0016>` in the DRS task as soon as possible to prevent automatic retry after a task failure. Automatic retry will lock the database accounts.

.. table:: **Table 2** Precautions

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Restrictions                                                                                                                                                                                                                                                                                                                                               |
   +===================================+============================================================================================================================================================================================================================================================================================================================================================+
   | Database permissions              | -  The source database DDM account must have at least one permission, for example, SELECT. The physical sharded database account must have the following permissions: SELECT, SHOW VIEW, EVENT, LOCK TABLES, REPLICATION SLAVE and REPLICATION CLIENT.                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | -  The destination database user must have the following permissions: SELECT, CREATE, ALTER, DROP, DELETE, INSERT, and UPDATE. The **root** account of the RDS for MySQL DB instance has the preceding permissions by default.                                                                                                                             |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Synchronization object            | -  Full synchronization supports the synchronization of data, table structures, and indexes.                                                                                                                                                                                                                                                               |
   |                                   | -  The source database cannot contain tables whose sharding keys are timestamp.                                                                                                                                                                                                                                                                            |
   |                                   | -  The sharding key of the source table must be added to the primary key and unique key of the destination table, which means that the primary key and unique key columns of the destination table must contain the sharded columns of the source table to avoid data conflict and inconsistency.                                                          |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Source database                   | -  During the incremental synchronization, the binlog of the source sharded database must be enabled and use the row-based format.                                                                                                                                                                                                                         |
   |                                   | -  If the storage space is sufficient, store the source database binlog for as long as possible. The recommended retention period is three days.                                                                                                                                                                                                           |
   |                                   | -  During an incremental synchronization, the **server_id** value of the MySQL source database must be set. If the source database version is MySQL 5.6 or earlier, the **server_id** value ranges from **2** to **4294967296**. If the source database is MySQL 5.7 or later, the **server_id** value ranges from **1** to **4294967296**.                |
   |                                   | -  The database names and table names of the source sharding middleware cannot contain the following characters: '<>/\\ and non-ASCII characters.                                                                                                                                                                                                          |
   |                                   | -  Enable **skip-name-resolve** for the MySQL source database to reduce the possibility of connection timeout.                                                                                                                                                                                                                                             |
   |                                   | -  Enable GTID of the source database.                                                                                                                                                                                                                                                                                                                     |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Destination database              | -  The destination database is an on-premises MySQL database.                                                                                                                                                                                                                                                                                              |
   |                                   | -  The destination DB instance must have sufficient storage space.                                                                                                                                                                                                                                                                                         |
   |                                   | -  If the destination database (excluding MySQL system database) has the same name as the source database, the table structures in the destination database must be consistent with those in the source database.                                                                                                                                          |
   |                                   | -  The character set of the destination database must be the same as that of the source database.                                                                                                                                                                                                                                                          |
   |                                   | -  The time zone of the destination database must be the same as that of the source database.                                                                                                                                                                                                                                                              |
   |                                   | -  During a synchronization, a large amount of data is written to the destination database. If the value of the **max_allowed_packet** parameter of the destination database is too small, data cannot be written. You are advised to set the **max_allowed_packet** parameter to a value greater than 100 MB.                                             |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Precautions                       | -  If the data types are incompatible, the synchronization may fail.                                                                                                                                                                                                                                                                                       |
   |                                   | -  If the source database contains a duplicate primary key or unique key, the data synchronized to the destination database will be less than that in the source database. Therefore, you must check and correct the data before starting the synchronization task.                                                                                        |
   |                                   | -  If the destination DB instance is an RDS for MySQL instance, tables encrypted using Transparent Data Encryption (TDE) cannot be synchronized.                                                                                                                                                                                                           |
   |                                   | -  If the destination MySQL database does not support TLS 1.2 or is a self-built database of an earlier version (earlier than 5.6.46 or between 5.7 and 5.7.28), you need to submit an O&M application for testing the SSL connection.                                                                                                                     |
   |                                   | -  The destination table can contain more columns than the source table. However, the following failures must be avoided:                                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                                                                            |
   |                                   |    -  Assume that extra columns on the destination cannot be null or have default values. If newly inserted data records are synchronized from the source to the destination, the extra columns will become null, which does not meet the requirements of the destination and will cause the task to fail.                                                 |
   |                                   |    -  Assume that extra columns on the destination must be fixed at a default value and have a unique constraint. If newly inserted data records are synchronized from the source to the destination, the extra columns will contain multiple default values. That does not meet the unique constraint of the destination and will cause the task to fail. |
   |                                   |                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | -  Resumable upload is supported, but data may be repeatedly inserted into a table that does not have a primary key when the server system breaks down.                                                                                                                                                                                                    |
   |                                   | -  After a task is created, the destination database cannot be set to read-only.                                                                                                                                                                                                                                                                           |
   |                                   | -  After a synchronization task is started, you are not allowed to add a schema or modify the association between the old schema and a new RDS DB instance. Otherwise, the synchronization task will fail.                                                                                                                                                 |
   |                                   | -  During synchronization, do not modify or delete the usernames, passwords, permissions, or ports of the source and destination databases.                                                                                                                                                                                                                |
   |                                   | -  During the synchronization, do not change the sharding key of a table on the source DDM instance, or change an unsharded or broadcast table to a sharded table, or change a sharded table to an unsharded or broadcast table.                                                                                                                           |
   |                                   | -  DDL operations are not supported during synchronization.                                                                                                                                                                                                                                                                                                |
   |                                   | -  During an incremental synchronization, do not modify the table structure to be synchronized in the source database.                                                                                                                                                                                                                                     |
   |                                   | -  During an incremental synchronization, do not perform the restoration operation on the source database.                                                                                                                                                                                                                                                 |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Procedure
---------

#. On the **Data Synchronization Management** page, click **Create Synchronization Task**.
#. On the **Create Synchronization Instance** page, specify the task name, description, and the synchronization instance details, and click **Next**.

   .. table:: **Table 3** Task and recipient description

      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter   | Description                                                                                                                                      |
      +=============+==================================================================================================================================================+
      | Region      | The region where your service is running. You can change the region.                                                                             |
      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | Project     | The project corresponds to the current region and can be changed.                                                                                |
      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | Task Name   | The task name must start with a letter and consist of 4 to 50 characters. It can contain only letters, digits, hyphens (-), and underscores (_). |
      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description | The description can contain up to 256 characters and cannot contain special characters ``!=<>&'\"``                                              |
      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

   .. table:: **Table 4** Synchronization instance details

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                |
      +===================================+============================================================================================================================================================================================================================================================================================================================+
      | Data Flow                         | Select **Out of the cloud**.                                                                                                                                                                                                                                                                                               |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Source DB Engine                  | Select **DDM**.                                                                                                                                                                                                                                                                                                            |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Destination DB Engine             | Select **MySQL**.                                                                                                                                                                                                                                                                                                          |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Network Type                      | The public network is used as an example. Available options: **VPC**, **Public network** and **VPN or Direct Connect**                                                                                                                                                                                                     |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Destination DB Instance           | The RDS instance you created.                                                                                                                                                                                                                                                                                              |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Instance Subnet   | Select the subnet where the synchronization instance is located. You can also click **View Subnets** to go to the network console to view the subnet where the instance resides.                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                                                                                            |
      |                                   | By default, the DRS instance and the destination DB instance are in the same subnet. You need to select the subnet where the DRS instance resides, and there are available IP addresses for the subnet. To ensure that the synchronization instance is successfully created, only subnets with DHCP enabled are displayed. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Mode              | -  **Full+Incremental**                                                                                                                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                                                                                                                            |
      |                                   |    This synchronization mode allows you to synchronize data in real time. After a full synchronization initializes the destination database, an incremental synchronization parses logs to ensure data consistency between the source and destination databases.                                                           |
      |                                   |                                                                                                                                                                                                                                                                                                                            |
      |                                   | -  **Full**                                                                                                                                                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                                                                                                                            |
      |                                   |    All objects and data in non-system databases are synchronized to the destination database at a time. This mode is applicable to scenarios where service interruption is acceptable.                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                                                                            |
      |                                   | -  **Incremental**                                                                                                                                                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                                                                            |
      |                                   |    Through log parsing, incremental data generated on the source database is synchronized to the destination database.                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                                                                            |
      |                                   | .. note::                                                                                                                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                                                                                            |
      |                                   |    If you select **Full+Incremental**, data generated during the full synchronization will be continuously synchronized to the destination database, and the source remains accessible.                                                                                                                                    |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Source DB Instance Quantity       | The default minimum number of source DB instances is 2. You can set this parameter based on the number of source database shards.                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                                                                            |
      |                                   | .. note::                                                                                                                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                                                                                            |
      |                                   |    After a task is created, DRS creates subtasks, whose quantity is the same as the number of source DB instances. Each subtask migrates data from its source database to the destination database.                                                                                                                        |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Specifications                    | DRS instance specifications. Different specifications have different performance upper limits. For details, see :ref:`Real-Time Synchronization <drs_01_0314>`.                                                                                                                                                            |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Tags                              | -  Tags a task. This configuration is optional. Adding tags helps you better identify and manage your tasks. Each task can have up to 20 tags.                                                                                                                                                                             |
      |                                   | -  After a task is created, you can view its tag details on the **Tags** tab. For details, see :ref:`Tag Management <drs_synchronization_tag>`.                                                                                                                                                                            |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      If a task fails to be created, DRS retains the task for three days by default. After three days, the task automatically ends.

#. On the **Configure Source and Destination Databases** page, wait until the synchronization instance is created. Then, specify source and destination database information and click **Test Connection** for both the source and destination databases to check whether they have been connected to the synchronization instance. After the connection tests are successful, select the check box before the agreement and click **Next**.

   .. table:: **Table 5** Source database information

      +-------------------+------------------------------------------------------------------------------------------------------------+
      | Parameter         | Description                                                                                                |
      +===================+============================================================================================================+
      | DB Instance Name  | The DDM instance you selected when you create a synchronization task. The instance name cannot be changed. |
      +-------------------+------------------------------------------------------------------------------------------------------------+
      | Database Username | The username for accessing the source database.                                                            |
      +-------------------+------------------------------------------------------------------------------------------------------------+
      | Database Password | The password for the database username.                                                                    |
      +-------------------+------------------------------------------------------------------------------------------------------------+

   .. note::

      The IP address, domain name, username, and password of the source database are encrypted and stored in DRS, and will be cleared after the task is deleted.

   .. table:: **Table 6** Destination database information

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                       |
      +===================================+===================================================================================================================================+
      | IP Address or Domain Name         | The IP address or domain name of the destination database.                                                                        |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
      | Port                              | The port of the destination database. Range: 1 - 65535                                                                            |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
      | Database Username                 | The username for accessing the destination database.                                                                              |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
      | Database Password                 | The password for the database username.                                                                                           |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
      | SSL Connection                    | SSL encrypts the connections between the source and destination databases. If SSL is enabled, upload the SSL CA root certificate. |
      |                                   |                                                                                                                                   |
      |                                   | This parameter is unavailable when the network type is VPC network and the database type is RDS DB instance.                      |
      |                                   |                                                                                                                                   |
      |                                   | .. note::                                                                                                                         |
      |                                   |                                                                                                                                   |
      |                                   |    -  The maximum size of a single certificate file that can be uploaded is 500 KB.                                               |
      |                                   |    -  If the SSL certificate is not used, your data may be at risk.                                                               |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+

#. On the **Set Synchronization Task** page, select the objects to be synchronized, and then click **Next**.

   .. table:: **Table 7** Synchronization mode and object

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                        |
      +===================================+====================================================================================================================================================================================================================+
      | Synchronization Object            | DRS supports table-level synchronization. You can select data for synchronization based on your service requirements. To quickly select the desired database objects, you can use the search function.             |
      |                                   |                                                                                                                                                                                                                    |
      |                                   | .. note::                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                    |
      |                                   |    -  You can search for table names to quickly select the required database objects.                                                                                                                              |
      |                                   |    -  If there are changes made to the source databases or objects, click in the upper right corner to update the objects to be synchronized.                                                                      |
      |                                   |                                                                                                                                                                                                                    |
      |                                   |    -  If an object name contains spaces, the spaces before and after the object name are not displayed. If there are two or more consecutive spaces in the middle of the object name, only one space is displayed. |
      |                                   |    -  The name of the selected synchronization object cannot contain spaces.                                                                                                                                       |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Check Task** page, check the synchronization task.

   -  If any check fails, review the cause and rectify the fault. After the fault is rectified, click **Check Again**.
   -  If all check items are successful, click **Next**.

      .. note::

         You can proceed to the next step only when all checks are successful. If there are any items that require confirmation, view and confirm the details first before proceeding to the next step.

#. On the **Confirm Task** page, specify **Start Time**, confirm that the configured information is correct, and click **Next**.

   .. table:: **Table 8** Task startup settings

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                 |
      +===================================+=============================================================================================================================================================================================+
      | Start Time                        | Set **Start Time** to **Start upon task creation** or **Start at a specified time** based on site requirements.                                                                             |
      |                                   |                                                                                                                                                                                             |
      |                                   | .. note::                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                             |
      |                                   |    After a synchronization task is started, the performance of the source and destination databases may be affected. You are advised to start a synchronization task during off-peak hours. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. After the task is submitted, you can view and manage it on the **Data Synchronization Management** page.

   -  You can view the task status. For more information about task status, see :ref:`Task Statuses <drs_06_0004>`.
   -  You can click |image1| in the upper-right corner to view the latest task status.
   -  By default, DRS retains a task in the **Configuration** state for three days. After three days, DRS automatically deletes background resources, but the task status remains unchanged. When you reconfigure the task, DRS applies for resources for the task again.

.. |image1| image:: /_static/images/en-us_image_0000002199576769.png
