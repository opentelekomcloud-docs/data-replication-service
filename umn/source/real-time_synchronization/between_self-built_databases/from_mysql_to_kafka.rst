:original_name: drs_04_0128.html

.. _drs_04_0128:

From MySQL to Kafka
===================

Supported Source and Destination Databases
------------------------------------------

.. table:: **Table 1** Supported databases

   +-----------------------------------+-----------------------------------+
   | Source DB                         | Destination DB                    |
   +===================================+===================================+
   | -  On-premises MySQL databases    | -  Kafka                          |
   | -  MySQL databases on an ECS      | -  DMS for Kafka                  |
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

.. table:: **Table 2** Precautions

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Restrictions                                                                                                                                                                                                                                                                                                                       |
   +===================================+====================================================================================================================================================================================================================================================================================================================================+
   | Database permissions              | -  The source database user must have the following permissions: SELECT, SHOW VIEW, EVENT, LOCK TABLES, REPLICATION SLAVE, REPLICATION CLIENT, and RELOAD.                                                                                                                                                                         |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Synchronization object            | -  The table data can be synchronized.                                                                                                                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                                                                                                                    |
   |                                   | -  Tables with storage engine different to MyISAM and InnoDB cannot be synchronized.                                                                                                                                                                                                                                               |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Source database                   | -  During the incremental synchronization, the binlog of the source MySQL database must be enabled and use the row-based format.                                                                                                                                                                                                   |
   |                                   | -  If the storage space is sufficient, store the source database binlog for as long as possible. The recommended retention period is three days.                                                                                                                                                                                   |
   |                                   | -  If the **expire_logs_days** value of the source database is set to **0**, the synchronization may fail.                                                                                                                                                                                                                         |
   |                                   | -  Enable GTID for the source database. If GTID is not enabled for the source database, primary/standby switchover is not supported. DRS tasks will be interrupted and cannot be restored during a switchover.                                                                                                                     |
   |                                   | -  During an incremental synchronization, the **server_id** value of the MySQL source database must be set. If the source database version is MySQL 5.6 or earlier, the **server_id** value ranges from **2** to **4294967296**. If the source database is MySQL 5.7, the **server_id** value ranges from **1** to **4294967296**. |
   |                                   | -  The database and table names in the source database cannot contain non-ASCII characters, or special characters '<`>/\\                                                                                                                                                                                                          |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Destination database              | -  The destination database is a Kafka database.                                                                                                                                                                                                                                                                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Precautions                       | -  Objects that have dependencies must be synchronized at the same time to avoid synchronization failure. Common dependencies: tables referenced by views, views referenced by views, views and tables referenced by stored procedures/functions/triggers, and tables referenced by primary and foreign keys                       |
   |                                   | -  Cascade operations cannot be performed on tables with foreign keys. If the foreign key index of a table is a common index, the table structure may fail to be created. You are advised to use a unique index.                                                                                                                   |
   |                                   | -  Binlogs cannot be forcibly deleted. Otherwise, the synchronization task fails.                                                                                                                                                                                                                                                  |
   |                                   | -  The source database does not support the **reset master** or **reset master to** command, which may cause DRS task failures or data inconsistency.                                                                                                                                                                              |
   |                                   | -  If the source MySQL database does not support TLS 1.2 or is a self-built database of an earlier version (earlier than 5.6.46 or between 5.7 and 5.7.28), you need to submit an O&M application for testing the SSL connection.                                                                                                  |
   |                                   | -  During the synchronization, do not delete or change the username, password, or permission of the source database, or change the port of the destination database.                                                                                                                                                               |
   |                                   | -  Data inconsistency may occur when the MyISAM table is modified during synchronization.                                                                                                                                                                                                                                          |
   |                                   | -  During synchronization of table-level objects, renaming tables is not recommended.                                                                                                                                                                                                                                              |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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
      | Data Flow                         | Choose **Self-built to self-built**.                                                                                                                                                                                                                                                                                   |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Source DB Engine                  | Select **MySQL**.                                                                                                                                                                                                                                                                                                      |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Destination DB Engine             | Select **Kafka**.                                                                                                                                                                                                                                                                                                      |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Network Type                      | The **Public network** is used as an example. Available options: **VPC**, **Public network** and **VPN or Direct Connect**                                                                                                                                                                                             |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | AZ                                | Select the AZ where you want to create the DRS instance. Selecting the one housing the source or destination database can provide better performance.                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                                                                                        |
      |                                   | If **Instance Type** is set to **primary/standby**, you can specify **Primary AZ** and **Standby AZ**.                                                                                                                                                                                                                 |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | VPC                               | Select an available VPC.                                                                                                                                                                                                                                                                                               |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Instance Subnet   | Select the subnet where the synchronization instance is located. You can also click **View Subnet** to go to the network console to view the subnet where the instance resides.                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                                                                                        |
      |                                   | By default, the DRS instance and the destination DB instance are in the same subnet. You need to select the subnet where the DRS instance resides and ensure that there are available IP addresses. To ensure that the synchronization instance is successfully created, only subnets with DHCP enabled are displayed. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Security Group                    | Select a security group. You can use security group rules to allow or deny access to the instance.                                                                                                                                                                                                                     |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Mode              | -  Incremental                                                                                                                                                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                                                                        |
      |                                   |    Through log parsing, incremental data generated on the source database is synchronized to the destination database.                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                                                        |
      |                                   |    During synchronization, the source database continues to provide services for external systems with zero downtime.                                                                                                                                                                                                  |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Tags                              | -  This setting is optional. Adding tags helps you better identify and manage your tasks. Each task can have up to 20 tags.                                                                                                                                                                                            |
      |                                   | -  After a task is created, you can view its tag details on the **Tags** tab. For details, see :ref:`Tag Management <drs_synchronization_tag>`.                                                                                                                                                                        |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      If a task fails to be created, DRS retains the task for three days by default. After three days, the task automatically ends.

#. On the **Configure Source and Destination Databases** page, wait until the synchronization instance is created. Then, specify source and destination database information and click **Test Connection** for both the source and destination databases to check whether they have been connected to the synchronization instance. After the connection tests are successful, select the check box before the agreement and click **Next**.

   .. table:: **Table 5** Source database settings

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

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                    |
      +===================================+================================================================================================================================================================================================================================================================+
      | Topic Synchronization Policy      | Topic synchronization policy. The options are as follows:                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                |
      |                                   | -  Select **A specified topic** if the data volume of the source database is small.                                                                                                                                                                            |
      |                                   | -  Select **Auto-generated topics** if each table contains a lot of data. Then, the system automatically generates a topic for each table.                                                                                                                     |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Topic                             | Select the topic to be synchronized to the destination database. This parameter is available when the topic is set to **A specified topic**.                                                                                                                   |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Topic Name Format                 | Topic name format. This parameter is available when **Topic Synchronization Policy** is set to **Auto-generated topics**.                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                |
      |                                   | Only variables **database** and **tablename** are supported. The other characters must be constants. Replace **$database$** with the database name and **$tablename$** with the table name.                                                                    |
      |                                   |                                                                                                                                                                                                                                                                |
      |                                   | For example, if this parameter is set to **$database$-$tablename$** and the database name is **db1**, and the table name is **tab1**, the topic name is **db1-tab1**. If DDL statements are synchronized, **$tablename$** is empty and the topic name is db1.  |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Number of Partitions              | This parameter is available when **Topic Synchronization Policy** is set to **Auto-generated topics**.                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                |
      |                                   | The number of partitions of a topic. Each topic can have multiple partitions. More partitions can provide higher throughput but consume more resources. Set the number of partitions based on the actual situation of brokers.                                 |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Replication Factor                | This parameter is available when **Topic Synchronization Policy** is set to **Auto-generated topics**.                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                |
      |                                   | Number of copies of a topic. Each topic can have multiple copies, and the copies are placed on different brokers in a cluster. The number of copies cannot exceed the number of brokers. Otherwise, the topic fails to be created.                             |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronize Topic To              | The policy for synchronizing topics to the Kafka partitions.                                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                                                                                                |
      |                                   | -  If topics are synchronized to different partitions by hash value of the database and table names, the performance on a single table query can be improved.                                                                                                  |
      |                                   | -  If topics are synchronized to partition 0, strong consistency can be obtained but write performance is impacted.                                                                                                                                            |
      |                                   | -  If topics are synchronized to different partitions by hash value of the primary key, one table corresponds to one topic. This prevents data from being written to the same partition, and consumers can obtain data from different partitions concurrently. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Data Format in Kafka              | Select the data format to be delivered from MySQL to Kafka.                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                                                                |
      |                                   | -  **JSON**: JSON message format, which is easy to interpret but takes up more space.                                                                                                                                                                          |
      |                                   | -  **JSON-C**: A data format that is compatible with multiple batch and stream computing frameworks.                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                                |
      |                                   | For details, see :ref:`Kafka Message Format <drs_03_0052>`.                                                                                                                                                                                                    |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronization Object            | Available options: **Tables** and **Databases**.                                                                                                                                                                                                               |
      |                                   |                                                                                                                                                                                                                                                                |
      |                                   | -  If the synchronization objects in source and destination databases have different names, you can map the source object name to the destination one. For details, see :ref:`Mapping Object Names <drs_10_0015>`.                                             |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Process Data** page, select the columns to be processed.

   -  If data processing is not required, click **Next**.
   -  If you need to process columns, set processing rules by referring to :ref:`Processing Data <drs_03_0035>`.

#. On the **Check Task** page, check the synchronization task.

   -  If any check fails, review the cause and rectify the fault. After the fault is rectified, click **Check Again**.
   -  If all check items are successful, click **Next**.

      .. note::

         You can proceed to the next step only when all checks are successful. If there are any items that require confirmation, view and confirm the details first before proceeding to the next step.

#. On the displayed page, specify **Start Time**, confirm that the configured information is correct, and click **Submit** to submit the task.

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

.. |image1| image:: /_static/images/en-us_image_0000001758549405.png
