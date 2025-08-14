:original_name: drs_04_0089.html

.. _drs_04_0089:

From MySQL to DDM
=================

Supported Source and Destination Databases
------------------------------------------

.. table:: **Table 1** Supported databases

   +---------------------------------------------------------+-----------------------------------+
   | Source DB                                               | Destination DB                    |
   +=========================================================+===================================+
   | -  On-premises databases (MySQL 5.5, 5.6, 5.7, and 8.0) | -  DDM instances                  |
   | -  ECS databases (MySQL 5.5, 5.6, 5.7, and 8.0)         |                                   |
   | -  Other cloud databases (MySQL 5.5, 5.6, 5.7, and 8.0) |                                   |
   | -  RDS for MySQL (5.5, 5.6, 5.7, 8.0)                   |                                   |
   +---------------------------------------------------------+-----------------------------------+

Supported Migration Objects
---------------------------

Different types of migration tasks support different migration objects. For details, see :ref:`Table 2 <drs_04_0089__table9915155511407>`. DRS will automatically check the objects you selected before the migration.

.. _drs_04_0089__table9915155511407:

.. table:: **Table 2** Migration objects

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Precautions                                                                                                                                                                                                         |
   +===================================+=====================================================================================================================================================================================================================+
   | Migration objects                 | -  Migration object level: table level                                                                                                                                                                              |
   |                                   | -  Supported migration objects:                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                     |
   |                                   |    -  Only the source database data can be migrated. The table structure and other database objects of the source database cannot be migrated.                                                                      |
   |                                   |    -  The system database and event statuses cannot be migrated.                                                                                                                                                    |
   |                                   |    -  Tables with storage engine different to MyISAM and InnoDB tables cannot be migrated.                                                                                                                          |
   |                                   |    -  Tables without primary keys cannot be migrated.                                                                                                                                                               |
   |                                   |    -  Cascade operations cannot be performed on tables with foreign keys. If the foreign key index of a table is a common index, the table structure may fail to be created. You are advised to use a unique index. |
   |                                   |                                                                                                                                                                                                                     |
   |                                   |    .. note::                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                     |
   |                                   |       The objects that can be migrated have the following constraints:                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                     |
   |                                   |       -  The names of the source databases and tables cannot contain non-ASCII characters, or special characters <'>`/\\"                                                                                           |
   |                                   |       -  The source database name cannot start with **ib_logfile** and cannot be **ib_buffer_pool**, **ib_doublewrite**, **ibdata1 or ibtmp1**.                                                                     |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Database Account Permission Requirements
----------------------------------------

To start a migration task, the source and destination database users must have permissions listed in the following table. Different types of migration tasks require different permissions. For details, see :ref:`Table 3 <drs_04_0089__table68938710614>`. DRS automatically checks the database account permissions in the pre-check phase and provides handling suggestions.

.. note::

   -  You are advised to create an independent database account for DRS task connection to prevent task failures caused by account modification.
   -  After changing the account passwords for the source and destination databases, :ref:`modify the connection information <drs_03_1135>` in the DRS task as soon as possible to prevent automatic retry after a task failure. Automatic retry will lock the database accounts.

.. _drs_04_0089__table68938710614:

.. table:: **Table 3** Database account permission

   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Type                      | Full Migration                                                                                                                                                                                    | Full+Incremental Migration                                                       |
   +===========================+===================================================================================================================================================================================================+==================================================================================+
   | Source database user      | The user must have the following minimum permissions:                                                                                                                                             | The user must have the following minimum permissions:                            |
   |                           |                                                                                                                                                                                                   |                                                                                  |
   |                           | SELECT, SHOW VIEW, and EVENT                                                                                                                                                                      | SELECT, SHOW VIEW, EVENT, LOCK TABLES, REPLICATION SLAVE, and REPLICATION CLIENT |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Destination database user | -  The DDM destination database user must have the following permissions: CREATE, DROP, ALTER, INDEX, INSERT, DELETE, UPDATE, and SELECT. In addition, grant the SELECT permission on all tables. |                                                                                  |
   |                           | -  The DDM destination database user must have the permission on the database to be migrated.                                                                                                     |                                                                                  |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+

.. _drs_04_0089__section14377146105411:

Suggestions
-----------

.. caution::

   -  When a task is being started or in the full migration phase, do not perform DDL operations on the source database. Otherwise, the task may be abnormal.
   -  To maintain data consistency before and after the migration, do not write data to the source and destination databases in the full migration mode. In the full+incremental migration mode, you can continue the migration while data is still being written to the source database.

-  The success of database migration depends on environment and manual operations. To ensure a smooth migration, perform a migration trial before you start the migration to help you detect and resolve problems in advance.

-  Start your migration task during off-peak hours. A less active database is easier to migrate successfully. If the data is fairly static, there is less likely to be any severe performance impacts during the migration.

   -  If network bandwidth is not limited, the query rate of the source database increases by about 50 MB/s during full migration, and two to four CPUs are occupied.

   -  The data being migrated may be locked by other transactions for a long period of time, resulting in read timeout.
   -  Due to the inherent characteristics of MySQL, in certain scenarios the performance may be negatively affected. For example, if the CPU resources are insufficient and the storage engine is TokuDB, the read speed on tables may be decreased by 10%.
   -  If DRS concurrently reads data from a database, it will use about 6 to 10 sessions. The impact of the connections on services must be considered.
   -  If you read a table, especially a large table, during the full migration, the exclusive lock on that table may be blocked.

-  Data-Level Comparison

   To obtain accurate comparison results, start data comparison at a specified time point during off-peak hours. If it is needed, select **Start at a specified time** for **Comparison Time**. Due to slight time difference and continuous operations on data, data inconsistency may occur, reducing the reliability and validity of the comparison results.

.. _drs_04_0089__section182303625619:

Precautions
-----------

The full+incremental migration process consists of four phases: task startup, full synchronization, incremental synchronization, and task completion. A single full migration task contains three phases. To ensure smooth migration, read the following precautions before creating a migration task.

.. table:: **Table 4** Precautions

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Restrictions                                                                                                                                                                                                                                                                                                                             |
   +===================================+==========================================================================================================================================================================================================================================================================================================================================+
   | Starting a task                   | -  **Source database requirements:**                                                                                                                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                                                                                                          |
   |                                   |    -  The binlog of the source database must be enabled and use the row-based format during incremental migration.                                                                                                                                                                                                                       |
   |                                   |    -  If the storage space is sufficient, store the source database binlogs for as long as possible. The recommended retention period is three days.                                                                                                                                                                                     |
   |                                   |    -  If the **expire_logs_days** value of the source database is set to **0**, the migration may fail. Set **expire_logs_day** to a proper value to ensure that the binlog does not expire before data transfer resumes. This ensures that services can be recovered after interruption.                                                |
   |                                   |    -  During an incremental migration, the **server_id** value of the MySQL source database must be set. If the source database version is MySQL 5.6 or earlier, the **server_id** value ranges from **2** to **4294967296**. If the source database is MySQL 5.7 or later, the **server_id** value ranges from **1** to **4294967296**. |
   |                                   |    -  Enable **skip-name-resolve** for the source database to reduce the possibility of connection timeout.                                                                                                                                                                                                                              |
   |                                   |    -  Enable GTID for the source database. If GTID is not enabled for the source database, primary/standby switchover is not supported. DRS tasks will be interrupted and cannot be restored during a switchover.                                                                                                                        |
   |                                   |    -  The **log_slave_updates** parameter of the source database must be enabled. Otherwise, the migration fails.                                                                                                                                                                                                                        |
   |                                   |    -  The **binlog_row_image** parameter value of the source database must be **FULL**. Otherwise, the migration fails.                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                                                          |
   |                                   | -  **Source database object requirements:**                                                                                                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                                                                                                          |
   |                                   |    -  If the source database is an on-premises database and has Percona Server for MySQL 5.6.x or Percona Server for MySQL 5.7.x installed, the memory manager must use Jemalloc to prevent Out of Memory errors caused by frequent queries on system tables.                                                                            |
   |                                   |    -  The source database does not support the **mysql binlog dump** command.                                                                                                                                                                                                                                                            |
   |                                   |    -  The source database does not support the **reset master** or **reset master to** command, which may cause DRS task failures or data inconsistency.                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                                                                                                                          |
   |                                   | -  **Destination database parameter requirements:**                                                                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                                          |
   |                                   |    -  The destination DB instance and associated RDS DB instance must be available. If the RDS DB instance type is primary/standby, the replication status must be normal.                                                                                                                                                               |
   |                                   |    -  The associated RDS DB instance must have sufficient storage space.                                                                                                                                                                                                                                                                 |
   |                                   |    -  The character set of the associated RDS database must be the same as that of the source database.                                                                                                                                                                                                                                  |
   |                                   |    -  The **AUTO_INCREMENT** value of a table in the destination cannot be less than that of a table in the source.                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                                          |
   |                                   | -  **Destination database object requirements:**                                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                                                          |
   |                                   |    -  To migrate table structures and other objects, you need to create table structures and indexes in the destination database based on table structures of the source schema. Objects that are not created in the destination database are not to be migrated.                                                                        |
   |                                   |    -  The table structure created in the destination database must be the same as that in the source database.                                                                                                                                                                                                                           |
   |                                   |    -  Ensure that the destination database is empty before starting the migration. Otherwise, data in the destination may be overwritten during incremental migration.                                                                                                                                                                   |
   |                                   |    -  If the destination DB instance uses columns of the TIMESTAMP or DATETIME data type as its sharding key, the seconds precision of the column is removed after the migration.                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                                          |
   |                                   | -  Other notes:                                                                                                                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                                                                          |
   |                                   |    -  If the data types are incompatible, the migration may fail.                                                                                                                                                                                                                                                                        |
   |                                   |    -  If the source and destination DB instances are RDS for MySQL instances, tables encrypted using Transparent Data Encryption (TDE) cannot be synchronized.                                                                                                                                                                           |
   |                                   |    -  If the source MySQL database does not support TLS 1.2 or is a self-built database of an earlier version (earlier than 5.6.46 or between 5.7 and 5.7.28), you need to submit an O&M application for testing the SSL connection.                                                                                                     |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Full migration                    | -  During task startup and full migration, do not perform DDL operations on the source database. Otherwise, the task may be abnormal.                                                                                                                                                                                                    |
   |                                   | -  During migration, do not modify or delete the usernames, passwords, permissions, or ports of the source and destination databases.                                                                                                                                                                                                    |
   |                                   | -  During migration, do not modify the destination database (including but not limited to DDL and DML operations) that is being migrated.                                                                                                                                                                                                |
   |                                   | -  During migration, do not clear the binlog in the source database.                                                                                                                                                                                                                                                                     |
   |                                   | -  During migration, do not create a database named **ib_logfile** in the source database.                                                                                                                                                                                                                                               |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Incremental migration             | -  During migration, do not modify or delete the usernames, passwords, permissions, or ports of the source and destination databases.                                                                                                                                                                                                    |
   |                                   | -  During migration, do not modify the destination database (including but not limited to DDL and DML operations) that is being migrated.                                                                                                                                                                                                |
   |                                   | -  During migration, do not clear the binlog in the source database.                                                                                                                                                                                                                                                                     |
   |                                   | -  During migration, do not create a database named **ib_logfile** on the source side.                                                                                                                                                                                                                                                   |
   |                                   | -  During an incremental migration of table-level objects, renaming tables is not supported.                                                                                                                                                                                                                                             |
   |                                   | -  During an incremental migration, do not perform the point-in-time recovery (PITR) operation on the source database.                                                                                                                                                                                                                   |
   |                                   | -  During an incremental migration, resumable upload is supported. However, data may be repeatedly inserted into a non-transactional table that does not have a primary key when the server system breaks down.                                                                                                                          |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Stopping a task                   | -  If the target DDM version is later than 3.0.4.1, DRS automatically updates the start value of the DDM sequence when the task is complete.                                                                                                                                                                                             |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Prerequisites
-------------

-  You have logged in to the DRS console.
-  For details about the DB types and versions supported by real-time migration, see :ref:`Real-Time Migration <drs_01_0301>`.

-  You have read :ref:`Suggestions <drs_04_0089__section14377146105411>` and :ref:`Precautions <drs_04_0089__section182303625619>`.

Procedure
---------

#. On the **Create Replication Instance** page, configure task details, description, and the replication instance, and click **Next**.

   -  Task information description

      .. table:: **Table 5** Task information

         +-------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter   | Description                                                                                                                                                               |
         +=============+===========================================================================================================================================================================+
         | Region      | The region where the replication instance is deployed. You can change the region. To reduce latency and improve access speed, select the region closest to your services. |
         +-------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Project     | The project corresponds to the current region and can be changed.                                                                                                         |
         +-------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Task Name   | The task name must start with a letter and consist of 4 to 50 characters. It can contain only letters, digits, hyphens (-), and underscores (_).                          |
         +-------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Description | The description consists of a maximum of 256 characters and cannot contain special characters ``!=<>'&"\``                                                                |
         +-------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   -  Replication instance information

      .. table:: **Table 6** Replication instance settings

         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                                                                                                                                                                                                                            |
         +===================================+========================================================================================================================================================================================================================================================================================================================+
         | Data Flow                         | Select **To the cloud**.                                                                                                                                                                                                                                                                                               |
         |                                   |                                                                                                                                                                                                                                                                                                                        |
         |                                   | The destination is a DB instance on the current cloud.                                                                                                                                                                                                                                                                 |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Source DB Engine                  | Select **MySQL**.                                                                                                                                                                                                                                                                                                      |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Destination DB Engine             | Select **DDM**.                                                                                                                                                                                                                                                                                                        |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Network Type                      | Available options: **VPC**, **Public network**, and **VPN or Direct Connect**. By default, the value is **Public network**.                                                                                                                                                                                            |
         |                                   |                                                                                                                                                                                                                                                                                                                        |
         |                                   | -  VPC is suitable for migrations of cloud databases in the same region.                                                                                                                                                                                                                                               |
         |                                   | -  VPN and Direct Connect are suitable for migrations from on-premises databases to cloud databases or between cloud databases across regions.                                                                                                                                                                         |
         |                                   | -  Public network is suitable for migration from on-premises databases or external cloud databases to destination databases.                                                                                                                                                                                           |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Destination DB Instance           | The DDM instance you created.                                                                                                                                                                                                                                                                                          |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Replication Instance Subnet       | The subnet where the replication instance resides. You can also click **View Subnet** to go to the network console to view the subnet where the instance resides.                                                                                                                                                      |
         |                                   |                                                                                                                                                                                                                                                                                                                        |
         |                                   | By default, the DRS instance and the destination DB instance are in the same subnet. You need to select the subnet where the DRS instance resides, and there are available IP addresses for the subnet. To ensure that the replication instance is successfully created, only subnets with DHCP enabled are displayed. |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Migration Type                    | -  **Full**: This migration type is suitable for scenarios where service interruption is acceptable. All objects in non-system databases are migrated to the destination database at one time, including tables, views, stored procedures, and triggers.                                                               |
         |                                   |                                                                                                                                                                                                                                                                                                                        |
         |                                   |    .. note::                                                                                                                                                                                                                                                                                                           |
         |                                   |                                                                                                                                                                                                                                                                                                                        |
         |                                   |       If you are performing a full migration, do not perform operations on the source database. Otherwise, data generated in the source database during the migration will not be synchronized to the destination database.                                                                                            |
         |                                   |                                                                                                                                                                                                                                                                                                                        |
         |                                   | -  **Full+Incremental**: This migration type allows you to migrate data without interrupting services. After a full migration initializes the destination database, an incremental migration initiates and parses logs to ensure data consistency between the source and destination databases.                        |
         |                                   |                                                                                                                                                                                                                                                                                                                        |
         |                                   |    .. note::                                                                                                                                                                                                                                                                                                           |
         |                                   |                                                                                                                                                                                                                                                                                                                        |
         |                                   |       If you select **Full+Incremental**, data generated during the full migration will be continuously synchronized to the destination database, and the source remains accessible.                                                                                                                                   |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   -  Tags

      .. table:: **Table 7** Tags

         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                                                    |
         +===================================+================================================================================================================================================+
         | Tags                              | -  Tags a task. This configuration is optional. Adding tags helps you better identify and manage your tasks. Each task can have up to 20 tags. |
         |                                   | -  After a task is created, you can view its tag details on the **Tags** tab. For details, see :ref:`Tag Management <drs_online_tag>`.         |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      If a task fails to be created, DRS retains the task for three days by default. After three days, the task automatically ends.

#. On the **Configure Source and Destination Databases** page, wait until the replication instance is created. Then, specify source and destination database information and click **Test Connection** for both the source and destination databases to check whether they have been connected to the replication instance. After the connection tests are successful, select the check box before the agreement and click **Next**.

   -  Source database configuration

      .. table:: **Table 8** Source database settings

         +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                                       |
         +===================================+===================================================================================================================================+
         | IP Address or Domain Name         | The IP address or domain name of the source database.                                                                             |
         +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
         | Port                              | The port of the source database. Range: 1 - 65535                                                                                 |
         +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
         | Database Username                 | The username for accessing the source database.                                                                                   |
         +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
         | Database Password                 | The password for the database username.                                                                                           |
         +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
         | SSL Connection                    | SSL encrypts the connections between the source and destination databases. If SSL is enabled, upload the SSL CA root certificate. |
         |                                   |                                                                                                                                   |
         |                                   | .. note::                                                                                                                         |
         |                                   |                                                                                                                                   |
         |                                   |    -  The maximum size of a single certificate file that can be uploaded is 500 KB.                                               |
         |                                   |    -  If the SSL certificate is not used, your data may be at risk.                                                               |
         +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+

      .. note::

         The IP address, domain name, username, and password of the source database are encrypted and stored in DRS, and will be cleared after the task is deleted.

   -  Destination database configuration

      .. table:: **Table 9** Destination database settings

         +-------------------+---------------------------------------------------------------------+
         | Parameter         | Description                                                         |
         +===================+=====================================================================+
         | DB Instance Name  | The DDM instance selected when you create the replication instance. |
         +-------------------+---------------------------------------------------------------------+
         | Database Username | The username for accessing the destination DDM database.            |
         +-------------------+---------------------------------------------------------------------+
         | Database Password | The password for the database username.                             |
         +-------------------+---------------------------------------------------------------------+

      .. note::

         The username and password of the destination database are encrypted and stored in DRS, and will be cleared after the task is deleted.

#. On the **Set Task** page, select migration objects and click **Next**.

   .. table:: **Table 10** Migration object

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                        |
      +===================================+====================================================================================================================================================================================================================+
      | Migrate Object                    | You can migrate table-level objects to destination databases based on service requirements.                                                                                                                        |
      |                                   |                                                                                                                                                                                                                    |
      |                                   | If the source database is changed, click |image1| in the upper right corner before selecting migration objects to ensure that the objects to be selected are from the changed source database.                     |
      |                                   |                                                                                                                                                                                                                    |
      |                                   | .. note::                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                    |
      |                                   |    -  If an object name contains spaces, the spaces before and after the object name are not displayed. If there are two or more consecutive spaces in the middle of the object name, only one space is displayed. |
      |                                   |    -  The name of the selected migration object cannot contain spaces.                                                                                                                                             |
      |                                   |    -  To quickly select the desired database objects, you can use the search function.                                                                                                                             |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Check Task** page, check the migration task.

   -  If any check fails, review the cause and rectify the fault. After the fault is rectified, click **Check Again**.

      For details about how to handle check items that fail to pass the pre-check, see :ref:`Solutions to Failed Check Items <drs_11_0001>`.

   -  If the check is complete and the check success rate is 100%, click **Next**.

      .. note::

         You can proceed to the next step only when all checks are successful. If there are any items that require confirmation, view and confirm the details first before proceeding to the next step.

#. On the **Confirm Task** page, specify **Start Time** and confirm that the configured information is correct and click **Submit** to submit the task.

   .. table:: **Table 11** Task startup settings

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                        |
      +===================================+====================================================================================================================================================================================================+
      | Started Time                      | Set **Start Time** to **Start upon task creation** or **Start at a specified time** based on site requirements. The **Start at a specified time** option is recommended.                           |
      |                                   |                                                                                                                                                                                                    |
      |                                   | .. note::                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                    |
      |                                   |    The migration task may affect the performance of the source and destination databases. You are advised to start the task in off-peak hours and reserve two to three days for data verification. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. After the task is submitted, view and manage it on the **Online Migration Management** page.

   -  You can view the task status. For more information about task status, see :ref:`Task Statuses <drs_03_0001>`.
   -  You can click |image2| in the upper right corner to view the latest task status.
   -  By default, DRS retains a task in the **Configuration** state for three days. After three days, DRS automatically deletes background resources, but the task status remains unchanged. When you reconfigure the task, DRS applies for resources for the task again.

.. |image1| image:: /_static/images/en-us_image_0000001758429473.png
.. |image2| image:: /_static/images/en-us_image_0000001758429809.png
