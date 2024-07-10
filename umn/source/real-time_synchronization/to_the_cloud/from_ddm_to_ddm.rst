:original_name: drs_04_0465.html

.. _drs_04_0465:

From DDM to DDM
===============

Supported Source and Destination Databases
------------------------------------------

.. table:: **Table 1** Supported databases

   +-----------------------------------+-----------------------------------+
   | Source DB                         | Destination DB                    |
   +===================================+===================================+
   | -  DDM instances                  | -  DDM instances                  |
   +-----------------------------------+-----------------------------------+

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
   -  The data being synchronized may be locked by other transactions for a long period of time, resulting in read timeout.
   -  When DRS concurrently reads data from a database, it will use about 6 to 10 sessions. The impact of the connections on services must be considered.
   -  If you read a table, especially a large table, during the full migration, the exclusive lock on that table may be blocked.

-  Data-Level Comparison

   To obtain accurate comparison results, start data comparison at a specified time point during off-peak hours. If it is needed, select **Start at a specified time** for **Comparison Time**. Due to slight time difference and continuous operations on data, data inconsistency may occur, reducing the reliability and validity of the comparison results.

Precautions
-----------

Before creating a synchronization task, read the following notes:

.. table:: **Table 2** Precautions

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Restrictions                                                                                                                                                                                                                                                                                                                                               |
   +===================================+============================================================================================================================================================================================================================================================================================================================================================+
   | Database permissions              | -  The source database DDM account must have the SELECT permission. The physical sharded database account must have the following permissions: SELECT, SHOW VIEW, EVENT, LOCK TABLES, REPLICATION SLAVE and REPLICATION CLIENT.                                                                                                                            |
   |                                   | -  The DDM destination database user must have the following permissions: CREATE, DROP, ALTER, INDEX, INSERT, DELETE, UPDATE, and SELECT. In addition, grant the select permission on all tables.                                                                                                                                                          |
   |                                   | -  The DDM destination database user must have the permission on the database to be synchronized.                                                                                                                                                                                                                                                          |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Synchronization object            | -  Full synchronization supports the synchronization of data, table structures, and indexes.                                                                                                                                                                                                                                                               |
   |                                   | -  The source database cannot contain tables whose sharding keys are timestamp.                                                                                                                                                                                                                                                                            |
   |                                   | -  Tables with storage engine different to MyISAM and InnoDB cannot be synchronized.                                                                                                                                                                                                                                                                       |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Source database                   | -  During the incremental synchronization, the binlog of the source sharded database must be enabled and use the row-based format.                                                                                                                                                                                                                         |
   |                                   | -  If the storage space is sufficient, store the source database binlog for as long as possible. The recommended retention period is three days.                                                                                                                                                                                                           |
   |                                   | -  During an incremental synchronization, the **server_id** value of the MySQL source database must be set. If the source database version is MySQL 5.6 or earlier, the **server_id** value ranges from **2** to **4294967296**. If the source database is MySQL 5.7 or later, the **server_id** value ranges from **1** to **4294967296**.                |
   |                                   | -  The database names and table names of the source sharding middleware cannot contain the following characters: '<>/\\ and non-ASCII characters.                                                                                                                                                                                                          |
   |                                   | -  Enable **skip-name-resolve** for the MySQL source database to reduce the possibility of connection timeout.                                                                                                                                                                                                                                             |
   |                                   | -  Enable GTID of the source database.                                                                                                                                                                                                                                                                                                                     |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Destination database              | -  Create a schema for the destination database in advance.                                                                                                                                                                                                                                                                                                |
   |                                   | -  Ensure that the destination database is empty before starting the synchronization. Otherwise, data in the destination may be overwritten during incremental synchronization.                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | -  The destination instance and associated RDS instance must be available. If the RDS instance type is primary/standby, the replication status must be normal.                                                                                                                                                                                             |
   |                                   | -  The associated RDS instance must have sufficient storage space.                                                                                                                                                                                                                                                                                         |
   |                                   | -  The character set of the associated RDS database must be the same as that of the source database.                                                                                                                                                                                                                                                       |
   |                                   | -  If the destination instance uses columns of the TIMESTAMP or DATETIME data type as its sharding key, the seconds precision of the column is removed after the synchronization.                                                                                                                                                                          |
   |                                   | -  The value of **AUTO_INCREMENT** of a table in the destination database cannot be less than that of **AUTO_INCREMENT** of a table in the source database.                                                                                                                                                                                                |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Precautions                       | -  If the data types are incompatible, the synchronization may fail.                                                                                                                                                                                                                                                                                       |
   |                                   | -  The destination table can contain more columns than the source table. However, the following failures must be avoided:                                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                                                                            |
   |                                   |    -  Assume that extra columns on the destination cannot be null or have default values. If newly inserted data records are synchronized from the source to the destination, the extra columns will become null, which does not meet the requirements of the destination and will cause the task to fail.                                                 |
   |                                   |    -  Assume that extra columns on the destination must be fixed at a default value and have a unique constraint. If newly inserted data records are synchronized from the source to the destination, the extra columns will contain multiple default values. That does not meet the unique constraint of the destination and will cause the task to fail. |
   |                                   |                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | -  During synchronization, do not modify or delete the usernames, passwords, permissions, or ports of the source and destination databases.                                                                                                                                                                                                                |
   |                                   | -  During synchronization, do not modify the table structure to be synchronized in the source database.                                                                                                                                                                                                                                                    |
   |                                   | -  During the synchronization, do not change the sharding key of a table on the source DDM instance, or change an unsharded or broadcast table to a sharded table, or change a sharded table to an unsharded or broadcast table.                                                                                                                           |
   |                                   | -  During an incremental synchronization, do not perform the restoration operation on the source database.                                                                                                                                                                                                                                                 |
   |                                   | -  During an incremental synchronization of table-level objects, renaming tables is not recommended.                                                                                                                                                                                                                                                       |
   |                                   | -  During the task startup or full synchronization, you are not advised to perform DDL operations, such as deletion, on the source database. Otherwise, the synchronization may fail.                                                                                                                                                                      |
   |                                   | -  If the target DDM version is later than 3.0.4.1, DRS automatically updates the start value of the DDM sequence when the task is complete.                                                                                                                                                                                                               |
   |                                   | -  Set the **expire_log_day** parameter for the physical shards of the source middleware to a proper value to ensure that the binlog at the breakpoint does not expire during restoration and that the service can be successfully restored after interruption.                                                                                            |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Procedure
---------

#. On the **Data Synchronization Management** page, click **Create Synchronization Task**.
#. On the **Create Synchronization Instance** page, specify the task name, description, and the synchronization instance details, and click **Next**.

   -  Task information description

      .. table:: **Table 3** Task and recipient description

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

   -  Synchronization instance information

      .. table:: **Table 4** Synchronization instance settings

         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                                                                                                                                                                                                                            |
         +===================================+========================================================================================================================================================================================================================================================================================================================+
         | Data Flow                         | Select **To the cloud**.                                                                                                                                                                                                                                                                                               |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Source DB Engine                  | Select **DDM**.                                                                                                                                                                                                                                                                                                        |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Destination DB Engine             | Select **DDM**.                                                                                                                                                                                                                                                                                                        |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Network Type                      | The public network is used as an example. Available options: **Public network**, **VPC**, **VPN or Direct Connect**                                                                                                                                                                                                    |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Destination DB Instance           | The DDM instance you created.                                                                                                                                                                                                                                                                                          |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Synchronization Instance Subnet   | Select the subnet where the synchronization instance is located. You can also click **View Subnet** to go to the network console to view the subnet where the instance resides.                                                                                                                                        |
         |                                   |                                                                                                                                                                                                                                                                                                                        |
         |                                   | By default, the DRS instance and the destination DB instance are in the same subnet. You need to select the subnet where the DRS instance resides and ensure that there are available IP addresses. To ensure that the synchronization instance is successfully created, only subnets with DHCP enabled are displayed. |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Synchronization Mode              | -  **Full+Incremental**                                                                                                                                                                                                                                                                                                |
         |                                   |                                                                                                                                                                                                                                                                                                                        |
         |                                   |    This synchronization mode allows you to synchronize data in real time. After a full synchronization initializes the destination database, an incremental synchronization parses logs to ensure data consistency between the source and destination databases.                                                       |
         |                                   |                                                                                                                                                                                                                                                                                                                        |
         |                                   | .. note::                                                                                                                                                                                                                                                                                                              |
         |                                   |                                                                                                                                                                                                                                                                                                                        |
         |                                   |    If you select **Full+Incremental**, data generated during the full synchronization will be continuously synchronized to the destination database, and the source remains accessible.                                                                                                                                |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Source DB Instance Quantity       | Specifies the number of DB instances bound to the source DDM database. The default value is 2. The value ranges from 1 to 64. Set this parameter based on the site requirements.                                                                                                                                       |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   -  Tags

      .. table:: **Table 5** Tags

         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                                                     |
         +===================================+=================================================================================================================================================+
         | Tags                              | -  This setting is optional. Adding tags helps you better identify and manage your tasks. Each task can have up to 20 tags.                     |
         |                                   | -  After a task is created, you can view its tag details on the **Tags** tab. For details, see :ref:`Tag Management <drs_synchronization_tag>`. |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Configure Source and Destination Databases** page, wait until the synchronization instance is created. Then, specify source and destination database information and click **Test Connection** for both the source and destination databases to check whether they have been connected to the synchronization instance. After the connection tests are successful, select the check box before the agreement and click **Next**.

   .. table:: **Table 6** Source database settings

      +--------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                            | Description                                                                                                                       |
      +======================================+===================================================================================================================================+
      | Middleware IP Address or Domain Name | The IP address or domain name of the source DDM middleware.                                                                       |
      +--------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
      | Port                                 | The port of the source DDM middleware. Value range: 1 to 65535                                                                    |
      +--------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
      | Middleware Username                  | The username of the source DDM instance.                                                                                          |
      +--------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
      | Middleware Password                  | The password for the source DDM instance username.                                                                                |
      +--------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
      | SSL Connection                       | SSL encrypts the connections between the source and destination databases. If SSL is enabled, upload the SSL CA root certificate. |
      |                                      |                                                                                                                                   |
      |                                      | .. note::                                                                                                                         |
      |                                      |                                                                                                                                   |
      |                                      |    -  The maximum size of a single certificate file that can be uploaded is 500 KB.                                               |
      |                                      |    -  If the SSL certificate is not used, your data may be at risk.                                                               |
      +--------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
      | DB Instance                          | The sharded database details.                                                                                                     |
      +--------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      The IP address, domain name, username, and password of the source database are encrypted and stored in DRS, and will be cleared after the task is deleted.

   .. table:: **Table 7** Destination database settings

      +-------------------+--------------------------------------------------------------------------------------------------------------------------+
      | Parameter         | Description                                                                                                              |
      +===================+==========================================================================================================================+
      | DB Instance Name  | The DDM instance you selected when you create a synchronization task. The instance name cannot be changed.               |
      +-------------------+--------------------------------------------------------------------------------------------------------------------------+
      | Database Username | The username for accessing the destination database.                                                                     |
      +-------------------+--------------------------------------------------------------------------------------------------------------------------+
      | Database Password | The database username and password are encrypted and stored in the system and will be cleared after the task is deleted. |
      +-------------------+--------------------------------------------------------------------------------------------------------------------------+

#. On the **Set Synchronization Task** page, select the objects to be synchronized, and then click **Next**.

   .. table:: **Table 8** Synchronization mode and object

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                     |
      +===================================+=================================================================================================================================================================================================================+
      | Incremental Conflict Policy       | The conflict policy refers to the conflict handling policy during incremental synchronization. By default, conflicts in the full synchronization phase are ignored.                                             |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Object            | Select **Tables** or **Databases** as required.                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                 |
      |                                   | If the synchronization objects in source and destination databases have different names, you can map the source object name to the destination one. For details, see :ref:`Mapping Object Names <drs_10_0015>`. |
      |                                   |                                                                                                                                                                                                                 |
      |                                   | .. note::                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                 |
      |                                   |    -  To quickly select the desired database objects, you can use the search function.                                                                                                                          |
      |                                   |    -  If there are changes made to the source databases or objects, click in the upper right corner to update the objects to be synchronized.                                                                   |
      |                                   |                                                                                                                                                                                                                 |
      |                                   |    -  If the object name contains spaces, the spaces before and after the object name are not displayed. If there are multiple spaces between the object name and the object name, only one space is displayed. |
      |                                   |    -  The name of the selected synchronization object cannot contain spaces.                                                                                                                                    |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Check Task** page, check the synchronization task.

   -  If any check fails, review the cause and rectify the fault. After the fault is rectified, click **Check Again**.
   -  If all check items are successful, click **Next**.

      .. note::

         You can proceed to the next step only when all checks are successful. If there are any items that require confirmation, view and confirm the details first before proceeding to the next step.

#. On the displayed page, specify **Start Time**, confirm that the configured information is correct, and click **Submit** to submit the task.

   .. table:: **Table 9** Task startup settings

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

.. |image1| image:: /_static/images/en-us_image_0000001758549405.png
