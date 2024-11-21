:original_name: drs_04_0121.html

.. _drs_04_0121:

From GaussDB Distributed to MySQL
=================================

Supported Source and Destination Databases
------------------------------------------

.. table:: **Table 1** Supported databases

   +-----------------------------------+------------------------------------------------------+
   | Source DB                         | Destination DB                                       |
   +===================================+======================================================+
   | -  GaussDB distributed            | -  RDS for MySQL 5.6 and 5.7                         |
   |                                   | -  On-premises MySQL 5.5, 5.6, and 5.7 databases     |
   |                                   | -  MySQL 5.5, 5.6, and 5.7 databases on an ECS       |
   |                                   | -  MySQL 5.5, 5.6, and 5.7 databases on other clouds |
   +-----------------------------------+------------------------------------------------------+

Supported Synchronization Objects
---------------------------------

:ref:`Table 2 <drs_04_0121__table3282654348>` lists the objects that can be synchronized in different scenarios. DRS will automatically check the objects you selected before the synchronization.

.. _drs_04_0121__table3282654348:

.. table:: **Table 2** Supported synchronization objects

   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Synchronization Scope                                                                                                                                                                                                                                                                                                                      |
   +===================================+============================================================================================================================================================================================================================================================================================================================================+
   | Synchronization scope             | -  Instance-level synchronization is not supported. Only one database can be synchronized at a time. To synchronize multiple databases, create multiple tasks.                                                                                                                                                                             |
   |                                   | -  **Supported scenario:** Incremental synchronization                                                                                                                                                                                                                                                                                     |
   |                                   | -  **Supported fields:** INTEGER, TINYINT, SMALLINT, BIGINT, NUMBER, NUMERIC, REAL, DOUBLE PRECISION, CHARACTER, CHARACTER VARYING, NVARCHAR2, BIT, BIT VARYING, BLOB, BYTEA, CLOB, RAW, TEXT, BOOLEAN, DATE, SMALLDATETIME, TIME WITH TIME ZONE, TIME WITHOUT TIME ZONE, TIMESTAMP WITH TIME ZONE, TIMESTAMP WITHOUT TIME ZONE and MONEY. |
   |                                   | -  **Table-level synchronization is supported.**                                                                                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                                                                                                                            |
   |                                   |    -  During incremental synchronization, only DML statements of selected tables can be synchronized.                                                                                                                                                                                                                                      |
   |                                   |    -  Databases without schemas cannot be synchronized.                                                                                                                                                                                                                                                                                    |
   |                                   |    -  Schemas without tables cannot be synchronized.                                                                                                                                                                                                                                                                                       |
   |                                   |    -  Column-store tables, compressed tables, delay tables, and temporary tables cannot be synchronized. Do not synchronize unlogged tables in the incremental phase.                                                                                                                                                                      |
   |                                   |    -  The database name, schema name, and table name cannot contain special characters :literal:`/<.>\\\\'`|\\?!`                                                                                                                                                                                                                          |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Database User Permission Requirements
-------------------------------------

Before you start a synchronization task, the source and destination database users must meet the requirements in the following table. Different types of synchronization tasks require different permissions. For details, see :ref:`Table 3 <drs_04_0121__table1480073518817>`. DRS automatically checks the database account permissions in the pre-check phase and provides handling suggestions.

.. _drs_04_0121__table1480073518817:

.. table:: **Table 3** Database user permission

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Incremental                                                                                                                                                                                                             |
   +===================================+=========================================================================================================================================================================================================================+
   | Source database user              | The user must have the sysadmin role or the following minimum permissions:                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                         |
   |                                   | -  The REPLICATION permission or the permission inherited from the built-in role **gs_role_replication**, the CONNECT permission for databases, the USAGE permission for schemas, and the SELECT permission for tables. |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Destination database user         | Required permissions:                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                         |
   |                                   | INSERT, DELETE, UPDATE, SELECT, and SHOW DATABASES                                                                                                                                                                      |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _drs_04_0121__section1113413054519:

Suggestions
-----------

.. caution::

   -  When a task is being started or in the full synchronization phase, do not perform DDL operations on the source database. Otherwise, the task may be abnormal.
   -  To keep data consistency before and after the synchronization, ensure that no data is written to the destination database during the synchronization.

-  The success of database synchronization depends on environment and manual operations. To ensure a smooth synchronization, perform a synchronization trial before you start the synchronization to help you detect and resolve problems in advance.

-  Start your synchronization task during off-peak hours. A less active database is easier to synchronize successfully. If the data is fairly static, there is less likely to be any severe performance impacts during the synchronization.

   -  The data being synchronized may be locked by other transactions for a long period of time, resulting in read timeout.
   -  When DRS concurrently reads data from a database, it will use about 6 to 10 sessions. The impact of the connections on services must be considered.

-  Data-Level Comparison

   To obtain accurate comparison results, compare data at a specified time point during off-peak hours. If it is needed, select **Start at a specified time** for **Comparison Time**. Due to slight time difference and continuous operations on data, data inconsistency may occur, reducing the reliability and validity of the comparison results.

.. _drs_04_0121__section449714073815:

Precautions
-----------

DRS incremental synchronization consists of three phases: task start, incremental synchronization, and task completion. To ensure smooth synchronization, read the following notes before creating a synchronization task.

.. table:: **Table 4** Precautions

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Restrictions                                                                                                                                                                                                                                                           |
   +===================================+========================================================================================================================================================================================================================================================================+
   | Starting a task                   | -  **Source database requirements:**                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                        |
   |                                   |    -  The **wal_level** parameter of the source database is set to **logical**.                                                                                                                                                                                        |
   |                                   |    -  The **enable_slot_log** parameter of the source database is set to **on**.                                                                                                                                                                                       |
   |                                   |    -  The **max_replication_slots** value of the source database must be greater than the number of used replication slots.                                                                                                                                            |
   |                                   |    -  Add a primary key to the table that does not have a primary key, or set REPLICA IDENTITY to FULL for the table that does not have a primary key.                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                                                        |
   |                                   | -  **Source database object requirements:**                                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                        |
   |                                   |    -  The names of the source database, schema, and table to be synchronized cannot contain special characters :literal:`/<.>\\\\'`|\\?!`                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                                        |
   |                                   | -  **Destination database parameter requirements:**                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                                        |
   |                                   |    -  The character set of the destination database must be the same as that of the source database.                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                        |
   |                                   | -  The destination database object must meet the following requirements:                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                        |
   |                                   |    -  The destination database has sufficient disk space.                                                                                                                                                                                                              |
   |                                   |    -  Before the synchronization, ensure that the corresponding database has been created in the destination instance.                                                                                                                                                 |
   |                                   |    -  Before synchronization, ensure that the table structure of the destination database has been created and is the same as that of the source database.                                                                                                             |
   |                                   |                                                                                                                                                                                                                                                                        |
   |                                   | -  **Other notes:**                                                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                                        |
   |                                   |    -  During real-time synchronization, the consistency of distributed transactions is not ensured.                                                                                                                                                                    |
   |                                   |    -  The table structure information is saved in uppercase in the source database. During synchronization, if the table names in the destination database are different from those in the source database, map the source table names to the destination table names. |
   |                                   |    -  If a logical replication slot fails to be created or does not exist due to a long transaction, you can reset the task and then restart it.                                                                                                                       |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Incremental synchronization       | -  Do not change the port of the source and destination databases, or change or delete the passwords and permissions of the source and destination database users. Otherwise, the task may fail.                                                                       |
   |                                   | -  Before a task enters the incremental synchronization phase, ensure that long-running transactions are not started in the source database. Starting the long transaction will block the creation of the logical replication slot and cause the task to fail.         |
   |                                   | -  Do not execute any DDL statement in the source database. Restricted by the GaussDB logical replication function, DDL statements cannot be synchronized. If you synchronize DDL statements, data may be inconsistent or the task may fail.                           |
   |                                   | -  Do not change the REPLICA IDENTITY value of a table in the source database. Otherwise, incremental data may be inconsistent or the task may fail.                                                                                                                   |
   |                                   | -  Do not write data to the destination database. Otherwise, data may be inconsistent.                                                                                                                                                                                 |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Synchronization comparison        | -  You are advised to compare data in the source database during off-peak hours to prevent inconsistent data from being falsely reported and reduce the impact on the source database and DRS tasks.                                                                   |
   |                                   | -  During incremental synchronization, if data is written to the source database, the comparison results may be inconsistent.                                                                                                                                          |
   |                                   | -  Do not limit the synchronization speed during data comparison.                                                                                                                                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Stopping a task                   | **Stop a task normally.**                                                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                                        |
   |                                   | -  After the task is complete, the streaming replication slot created in the source database is automatically deleted.                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                                                        |
   |                                   | **Forcibly stop a task.**                                                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                                        |
   |                                   | -  To forcibly stop a synchronization task, you need to manually delete the replication slots that may remain in the source database. For details, see :ref:`Forcibly Stopping Synchronization of GaussDB Distributed <drs_03_1131>`.                                  |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Prerequisites
-------------

-  You have logged in to the DRS console.
-  For details about the DB types and versions supported by real-time synchronization, see :ref:`Real-Time Synchronization <drs_01_0302>`.

-  You have read :ref:`Suggestions <drs_04_0121__section1113413054519>` and :ref:`Precautions <drs_04_0121__section449714073815>`.

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
      | Source DB Engine                  | Select **GaussDB Distributed Edition**.                                                                                                         |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Destination DB Engine             | Select **MySQL**.                                                                                                                               |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Network Type                      | The public network is used as an example. Available options: **Public network** and **VPN or Direct Connect**                                   |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Source DB Instance                | The GaussDB distributed instance you created.                                                                                                   |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Mode              | -  **Incremental**                                                                                                                              |
      |                                   |                                                                                                                                                 |
      |                                   |    Through log parsing, incremental data generated on the source database is synchronized to the destination database.                          |
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
      | DB Instance Name  | The GaussDB distributed instance selected during synchronization task creation. This parameter cannot be changed. |
      +-------------------+-------------------------------------------------------------------------------------------------------------------+
      | Database Username | The username for accessing the source database.                                                                   |
      +-------------------+-------------------------------------------------------------------------------------------------------------------+
      | Database Password | The password for the database username.                                                                           |
      +-------------------+-------------------------------------------------------------------------------------------------------------------+

   .. note::

      The username and password of the source database are encrypted and stored in the database and the synchronization instance during the synchronization. After the task is deleted, the username and password are permanently deleted.

   .. table:: **Table 8** Destination database settings

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                 |
      +===================================+=============================================================================================================================================================+
      | IP Address or Domain Name         | IP address or domain name of the destination database in the **IP address/Domain name:Port** format. The port of the destination database. Range: 1 - 65535 |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Port                              | The port of the destination database. Range: 1 - 65535                                                                                                      |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Database Username                 | The username for accessing the destination database.                                                                                                        |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Database Password                 | The password for the database username.                                                                                                                     |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | SSL Connection                    | SSL encrypts the connections between the source and destination databases. If SSL is enabled, upload the SSL CA root certificate.                           |
      |                                   |                                                                                                                                                             |
      |                                   | .. note::                                                                                                                                                   |
      |                                   |                                                                                                                                                             |
      |                                   |    -  The maximum size of a single certificate file that can be uploaded is 500 KB.                                                                         |
      |                                   |    -  If SSL is disabled, your data may be at risk.                                                                                                         |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      The username and password of the destination database are encrypted and stored in the database and the synchronization instance during the synchronization. After the task is deleted, the username and password are permanently deleted.

#. On the **Set Synchronization Task** page, select the objects to be synchronized, and then click **Next**.

   .. table:: **Table 9** Synchronization Object

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                        |
      +===================================+====================================================================================================================================================================================================================+
      | Incremental Conflict Policy       | The conflict policy refers to the conflict handling policy during incremental synchronization. By default, conflicts in the full synchronization phase are ignored. Select any of the following conflict policies: |
      |                                   |                                                                                                                                                                                                                    |
      |                                   | -  Ignore                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                    |
      |                                   |    The system will skip the conflicting data and continue the subsequent synchronization process.                                                                                                                  |
      |                                   |                                                                                                                                                                                                                    |
      |                                   | -  Report error                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                    |
      |                                   |    The synchronization task will be stopped and fail.                                                                                                                                                              |
      |                                   |                                                                                                                                                                                                                    |
      |                                   | -  Overwrite                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                    |
      |                                   |    Conflicting data will be overwritten.                                                                                                                                                                           |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Object            | DRS supports table-level synchronization. You can select data for synchronization based on your service requirements.                                                                                              |
      |                                   |                                                                                                                                                                                                                    |
      |                                   | If the synchronization objects in source and destination databases have different names, you can map the source object name to the destination one. For details, see :ref:`Mapping Object Names <drs_10_0015>`.    |
      |                                   |                                                                                                                                                                                                                    |
      |                                   | .. note::                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                    |
      |                                   |    -  To quickly select the desired database objects, you can use the search function.                                                                                                                             |
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

.. |image1| image:: /_static/images/en-us_image_0000001758549405.png
