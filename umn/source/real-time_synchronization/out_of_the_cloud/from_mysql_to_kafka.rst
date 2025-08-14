:original_name: drs_04_0118.html

.. _drs_04_0118:

From MySQL to Kafka
===================

Supported Source and Destination Databases
------------------------------------------

.. table:: **Table 1** Supported databases

   +-----------------------------------+-----------------------------------+
   | Source DB                         | Destination DB                    |
   +===================================+===================================+
   | -  RDS for MySQL                  | -  Kafka                          |
   +-----------------------------------+-----------------------------------+

Prerequisites
-------------

-  You have logged in to the DRS console.
-  For details about the DB types and versions supported by real-time synchronization, see :ref:`Real-Time Synchronization <drs_01_0302>`.

Suggestions
-----------

-  The success of database synchronization depends on environment and manual operations. To ensure a smooth synchronization, perform a synchronization trial before you start the synchronization to help you detect and resolve problems in advance.
-  It is recommended that you start a task during off-peak hours to minimize the impact of synchronization on your services.

Precautions
-----------

Before creating a synchronization task, read the following notes:

.. note::

   -  You are advised to create an independent database account for DRS task connection to prevent task failures caused by account modification.
   -  After changing the account passwords for the source or destination databases, :ref:`modify the connection information <drs_10_0016>` in the DRS task as soon as possible to prevent automatic retry after a task failure. Automatic retry will lock the database accounts.

.. table:: **Table 2** Precautions

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Restrictions                                                                                                                                                                                                                                                                                                                                |
   +===================================+=============================================================================================================================================================================================================================================================================================================================================+
   | Database permissions              | -  The source database user must have the following permissions: SELECT, LOCK TABLES, REPLICATION SLAVE, REPLICATION CLIENT, and RELOAD.                                                                                                                                                                                                    |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Synchronization object            | -  The table data can be synchronized.                                                                                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                                             |
   |                                   | -  Tables with storage engine different to MyISAM and InnoDB cannot be synchronized.                                                                                                                                                                                                                                                        |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Source database                   | -  During the incremental synchronization, the binlog of the source MySQL database must be enabled and use the row-based format.                                                                                                                                                                                                            |
   |                                   | -  If the storage space is sufficient, store the source database binlog for as long as possible. The recommended retention period is three days.                                                                                                                                                                                            |
   |                                   | -  If the **expire_logs_days** value of the source database is set to **0**, the synchronization may fail.                                                                                                                                                                                                                                  |
   |                                   | -  Enable GTID for the source database. If GTID is not enabled for the source database, primary/standby switchover is not supported. DRS tasks will be interrupted and cannot be restored during a switchover.                                                                                                                              |
   |                                   | -  During an incremental synchronization, the **server_id** value of the MySQL source database must be set. If the source database version is MySQL 5.6 or earlier, the **server_id** value ranges from **2** to **4294967296**. If the source database is MySQL 5.7 or later, the **server_id** value ranges from **1** to **4294967296**. |
   |                                   | -  The database and table names in the source database cannot contain non-ASCII characters, or special characters '<`>/\\                                                                                                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Destination database              | -  The destination database is a Kafka database.                                                                                                                                                                                                                                                                                            |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Precautions                       | -  If the data types are incompatible, the synchronization may fail.                                                                                                                                                                                                                                                                        |
   |                                   | -  If the source DB instance is an RDS for MySQL instance, tables encrypted using Transparent Data Encryption (TDE) cannot be synchronized.                                                                                                                                                                                                 |
   |                                   | -  A real-time synchronization task may fail due to the change of the username and password of the source database. You need to rectify the information and then retry the synchronization task on the DRS console. Generally, you are advised not to modify the preceding information during synchronization.                              |
   |                                   | -  If the source database port is changed during data synchronization, the synchronization task fails. If the destination database port is wrong, DRS automatically changes the port to the correct one, and then you need to retry the synchronization task. Generally, do not modify the port number during synchronization.              |
   |                                   | -  If a real-time synchronization task fails as the IP address is changed, the system automatically changes the IP address to the correct one. Then, you need to retry the task to continue the synchronization. Therefore, changing the IP address is not recommended.                                                                     |
   |                                   | -  Cascade operations cannot be performed on tables with foreign keys. If the foreign key index of a table is a common index, the table structure may fail to be created. You are advised to use a unique index.                                                                                                                            |
   |                                   | -  The source database does not support point-in-time recovery (PITR).                                                                                                                                                                                                                                                                      |
   |                                   | -  Resumable upload is supported, but data may be repeatedly inserted into a table that does not have a primary key.                                                                                                                                                                                                                        |
   |                                   | -  Binlogs cannot be forcibly deleted. Otherwise, the synchronization task fails.                                                                                                                                                                                                                                                           |
   |                                   | -  The source database does not support the **reset master** or **reset master to** command, which may cause DRS task failures or data inconsistency.                                                                                                                                                                                       |
   |                                   | -  Data inconsistency may occur when the MyISAM table is modified during synchronization.                                                                                                                                                                                                                                                   |
   |                                   | -  During synchronization of table-level objects, renaming tables is not recommended.                                                                                                                                                                                                                                                       |
   |                                   | -  Set the **expire_log_day** parameter to a proper value to ensure that the binlog does not expire before data transfer resumes. This ensures that services can be recovered after interruption.                                                                                                                                           |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Procedure
---------

#. On the **Data Synchronization Management** page, click **Create Synchronization Task**.
#. On the **Create Synchronization Instance** page, specify the task name, description, and the synchronization instance details, and click **Next**.

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

   .. table:: **Table 4** Synchronization instance settings

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                            |
      +===================================+========================================================================================================================================================================================================================================================================================================================+
      | Data Flow                         | Select **Out of the cloud**.                                                                                                                                                                                                                                                                                           |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Source DB Engine                  | Select **MySQL**.                                                                                                                                                                                                                                                                                                      |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Destination DB Engine             | Select **Kafka**.                                                                                                                                                                                                                                                                                                      |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Network Type                      | The **Public network** is used as an example. Available options: **Public network**, **VPC**, **VPN or Direct Connect**                                                                                                                                                                                                |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Source DB Instance                | The RDS for MySQL instance you created.                                                                                                                                                                                                                                                                                |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Instance Subnet   | Select the subnet where the synchronization instance is located. You can also click **View Subnet** to go to the network console to view the subnet where the instance resides.                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                                                                                        |
      |                                   | By default, the DRS instance and the destination DB instance are in the same subnet. You need to select the subnet where the DRS instance resides and ensure that there are available IP addresses. To ensure that the synchronization instance is successfully created, only subnets with DHCP enabled are displayed. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Mode              | -  Incremental                                                                                                                                                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                                                                        |
      |                                   |    Through log parsing, incremental data generated on the source database is synchronized to the destination database.                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                                                        |
      |                                   |    During synchronization, the source database continues to provide services for external systems with zero downtime.                                                                                                                                                                                                  |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Specifications                    | DRS instance specifications. Different specifications have different performance upper limits. For details, see :ref:`Real-Time Synchronization <drs_01_0314>`.                                                                                                                                                        |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Tags                              | -  This setting is optional. Adding tags helps you better identify and manage your tasks. Each task can have up to 20 tags.                                                                                                                                                                                            |
      |                                   | -  After a task is created, you can view its tag details on the **Tags** tab. For details, see :ref:`Tag Management <drs_synchronization_tag>`.                                                                                                                                                                        |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      If a task fails to be created, DRS retains the task for three days by default. After three days, the task automatically ends.

#. On the **Configure Source and Destination Databases** page, wait until the synchronization instance is created. Then, specify source and destination database information and click **Test Connection** for both the source and destination databases to check whether they have been connected to the synchronization instance. After the connection tests are successful, select the check box before the agreement and click **Next**.

   .. table:: **Table 5** Source database settings

      +-------------------+------------------------------------------------------------------------------------------------------+
      | Parameter         | Description                                                                                          |
      +===================+======================================================================================================+
      | DB Instance Name  | The RDS DB instance selected during synchronization task creation. This parameter cannot be changed. |
      +-------------------+------------------------------------------------------------------------------------------------------+
      | Database Username | The username for accessing the source database.                                                      |
      +-------------------+------------------------------------------------------------------------------------------------------+
      | Database Password | The password for the database username.                                                              |
      +-------------------+------------------------------------------------------------------------------------------------------+

   .. note::

      The username and password of the source database are encrypted and stored in DRS and will be cleared after the task is deleted.

   .. table:: **Table 6** Source database information

      +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                 | Description                                                                                                                                  |
      +===========================+==============================================================================================================================================+
      | IP Address or Domain Name | The IP address or domain name of the destination database.                                                                                   |
      +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | Security Protocol         | Available options: **PLAINTEXT**, **SSL**, **SASL_PLAINTEXT**, and **SASL_SSL**. For details, see :ref:`Kafka Authentication <drs_05_0018>`. |
      +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Set Synchronization Task** page, select the synchronization policy, objects, and data format, and click **Next**.

   .. table:: **Table 7** Synchronization Object

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                   |
      +===================================+===============================================================================================================================================================================================================================================================+
      | Synchronize DML                   | Select the DML operations to be synchronized. By default, all DML operations are selected.                                                                                                                                                                    |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Topic Synchronization Policy      | Topic synchronization policy. You can select **A specific topic** or **Auto-generated topics**.                                                                                                                                                               |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Topic                             | Select the topic to be synchronized to the destination database. This parameter is available when the topic is set to **A specified topic**.                                                                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Topic Name Format                 | Topic name format. This parameter is available when **Topic Synchronization Policy** is set to **Auto-generated topics**.                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                               |
      |                                   | Only variables **database** and **tablename** are supported. The other characters must be constants. Replace **$database$** with the database name and **$tablename$** with the table name.                                                                   |
      |                                   |                                                                                                                                                                                                                                                               |
      |                                   | For example, if this parameter is set to **$database$-$tablename$** and the database name is **db1**, and the table name is **tab1**, the topic name is **db1-tab1**. If DDL statements are synchronized, **$tablename$** is empty and the topic name is db1. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Number of Partitions              | This parameter is available when **Topic Synchronization Policy** is set to **Auto-generated topics**.                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                               |
      |                                   | The number of partitions of a topic. Each topic can have multiple partitions. More partitions can provide higher throughput but consume more resources. Set the number of partitions based on the actual situation of brokers.                                |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Replication Factor                | This parameter is available when **Topic Synchronization Policy** is set to **Auto-generated topics**.                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                               |
      |                                   | Number of copies of a topic. Each topic can have multiple copies, and the copies are placed on different brokers in a cluster. The number of copies cannot exceed the number of brokers. Otherwise, the topic fails to be created.                            |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronize Topic To              | The policy for synchronizing topics to the Kafka partitions.                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                               |
      |                                   | -  If topics are synchronized to different partitions by hash value of the database and table names, the performance on a single table query can be improved.                                                                                                 |
      |                                   | -  If topics are synchronized to partition 0, strong consistency can be obtained but write performance is impacted. If you select **Partition 0**, only automatically created topics can be synchronized.                                                     |
      |                                   | -  If topics are synchronized to different partitions by hash value of the primary key, one table corresponds to one topic.                                                                                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Data Format in Kafka              | Select the data format to be delivered from MySQL to Kafka.                                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                                                                                               |
      |                                   | -  **JSON**: JSON message format, which is easy to interpret but takes up more space.                                                                                                                                                                         |
      |                                   | -  **JSON-C**: A data format that is compatible with multiple batch and stream computing frameworks.                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                               |
      |                                   | For details, see :ref:`Kafka Message Format <drs_03_0052>`.                                                                                                                                                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Object            | Available options: **Tables** or **Databases** as required.                                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                                                                                               |
      |                                   | -  If the synchronization objects in source and destination databases have different names, you can map the source object name to the destination one. For details, see :ref:`Changing Object Names (Mapping Object Names) <drs_10_0015>`.                    |
      |                                   |                                                                                                                                                                                                                                                               |
      |                                   | .. note::                                                                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                               |
      |                                   |    -  You can search for table names to quickly select the required database objects.                                                                                                                                                                         |
      |                                   |    -  If there are changes made to the source databases or objects, click in the upper right corner to update the objects to be synchronized.                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                               |
      |                                   |    -  If an object name contains spaces, the spaces before and after the object name are not displayed. If there are two or more consecutive spaces in the middle of the object name, only one space is displayed.                                            |
      |                                   |    -  The name of the selected synchronization object cannot contain spaces.                                                                                                                                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Process Data** page, select the columns to be processed.

   -  If data processing is not required, click **Next**.
   -  If you need to process columns, set processing rules by referring to :ref:`Processing Data <drs_03_0035>`.

#. On the **Check Task** page, check the synchronization task.

   -  If any check fails, review the cause and rectify the fault. After the fault is rectified, click **Check Again**.
   -  If all check items are successful, click **Next**.

      .. note::

         You can proceed to the next step only when all checks are successful. If there are any items that require confirmation, view and confirm the details first before proceeding to the next step.

#. On the **Confirm Task** page, specify **Start Time**, confirm that the configured information is correct, and click **Submit** to submit the task.

   .. table:: **Table 8** Task startup settings

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
