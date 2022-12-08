:original_name: drs_02_0010.html

.. _drs_02_0010:

Creating an RDS Backup Migration Task
=====================================

Supported Source and Destination Databases
------------------------------------------

.. table:: **Table 1** Supported databases

   +-----------------------------------------------------+-----------------------------------+
   | Backup File                                         | Destination DB                    |
   +=====================================================+===================================+
   | RDS Microsoft SQL Server full backup file versions: | RDS for Microsoft SQL Server      |
   |                                                     |                                   |
   | -  Microsoft SQL Server 2008                        | -  Microsoft SQL Server 2008      |
   | -  Microsoft SQL Server 2012                        | -  Microsoft SQL Server 2012      |
   | -  Microsoft SQL Server 2014                        | -  Microsoft SQL Server 2014      |
   | -  Microsoft SQL Server 2016                        | -  Microsoft SQL Server 2016      |
   | -  Microsoft SQL Server 2017                        | -  Microsoft SQL Server 2017      |
   | -  Microsoft SQL Server 2019                        | -  Microsoft SQL Server 2019      |
   +-----------------------------------------------------+-----------------------------------+

Prerequisites
-------------

-  You have logged in to the DRS console.
-  For details about the supported DB types and versions, see :ref:`Backup Migration <drs_01_0303>`.

Precautions
-----------

This section describes constraints on backup migrations of Microsoft SQL Server databases.

.. table:: **Table 2** Precautions

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Restrictions                                                                                                                                                                                                        |
   +===================================+=====================================================================================================================================================================================================================+
   | Database permissions              | Before creating a backup migration task, ensure that the account has the permission to operate the RDS service.                                                                                                     |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Backup database names             | -  Backup database names are case-insensitive, must be unique, and cannot be any of the following:                                                                                                                  |
   |                                   |                                                                                                                                                                                                                     |
   |                                   |    -  msdb                                                                                                                                                                                                          |
   |                                   |    -  master                                                                                                                                                                                                        |
   |                                   |    -  model                                                                                                                                                                                                         |
   |                                   |    -  tempdb                                                                                                                                                                                                        |
   |                                   |    -  rdsadmin                                                                                                                                                                                                      |
   |                                   |    -  resource                                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | New database name                 | -  The new database name must be unique and cannot be any of the following (case-insensitive):                                                                                                                      |
   |                                   |                                                                                                                                                                                                                     |
   |                                   |    -  msdb                                                                                                                                                                                                          |
   |                                   |    -  master                                                                                                                                                                                                        |
   |                                   |    -  model                                                                                                                                                                                                         |
   |                                   |    -  tempdb                                                                                                                                                                                                        |
   |                                   |    -  rdsadmin                                                                                                                                                                                                      |
   |                                   |    -  resource                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                     |
   |                                   | -  The new database name contains 1 to 128 characters, including letters, digits, underscores (_), and hyphens (-).                                                                                                 |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Backup file sources               | -  RDS full backups: Backup files are manually or automatically created for RDS DB instances.                                                                                                                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Precautions                       | -  The available disk space of the destination database is at least 1.5 times the total data size of the backup database.                                                                                           |
   |                                   | -  Backup database name is case-sensitive and must be the same as the database name in the backup file.                                                                                                             |
   |                                   | -  The database backup file from a database of later version cannot be restored on the instance database of an earlier version (for example, restored from version 2017 to 2016).                                   |
   |                                   | -  The restoration from Enterprise Edition to Standard Edition to Web Edition may fail. That depends on whether the features of the later version are enabled.                                                      |
   |                                   | -  During a migration, if **Overwrite Data** is set to **Yes**, high availability of the destination database is disabled by default. After the migration is complete, high availability is restored automatically. |
   |                                   | -  During a migration, stop writing transactions to the destination database.                                                                                                                                       |
   |                                   | -  If a primary/standby switchover of the destination database is performed, the backup migration fails. In this case, the migration task cannot be restored.                                                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Procedure
---------

This section describes how to create an RDS full backup migration task. You can use the full backups of Microsoft SQL Server DB instances in the cloud to migrate data.

#. On the **Backup Migration Management** page, click **Create Migration Task**.
#. On the **Select Backup** page, specify information about the task and backup files. Then, click **Next**.

   .. table:: **Table 3** Task information

      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter   | Description                                                                                                                                      |
      +=============+==================================================================================================================================================+
      | Task Name   | The task name must start with a letter and consist of 4 to 50 characters. It can contain only letters, digits, hyphens (-), and underscores (_). |
      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description | The description consists of a maximum of 256 characters and cannot contain special characters ``!=<>'&"\``                                       |
      +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

   .. table:: **Table 4** Backup file information

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                         |
      +===================================+=====================================================================================================================================+
      | Database Type                     | Select **Microsoft SQL Server**.                                                                                                    |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
      | Backup File Source                | Select **RDS full backup**.                                                                                                         |
      |                                   |                                                                                                                                     |
      |                                   | .. note::                                                                                                                           |
      |                                   |                                                                                                                                     |
      |                                   |    Select a backup file whose status is **Completed**.                                                                              |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
      | Tags                              | This setting is optional. Adding tags helps you better identify and manage your tasks. Each task can have up to 20 tags.            |
      |                                   |                                                                                                                                     |
      |                                   | After a task is created, you can view its tag details on the **Tags** tab. For details, see :ref:`Tag Management <drs_backup_tag>`. |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Select Destination** page, specify database information and click **Next**.

   .. table:: **Table 5** Database information

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                  |
      +===================================+==============================================================================================================================================================================================================================================================+
      | Destination RDS DB Instance Name  | Select a destination RDS DB instance. If no RDS DB instance is available, you can create one.                                                                                                                                                                |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Backup Database Name              | After you select the destination RDS DB instance, all databases to be restored are automatically displayed. You can select databases to be restored as required and rename them.                                                                             |
      |                                   |                                                                                                                                                                                                                                                              |
      |                                   | -  **Backup Database Name**: Name of the database to be restored.                                                                                                                                                                                            |
      |                                   | -  **New Database Name**: The backup database name must consist of 1 to 64 characters. It can contain only uppercase letters, lowercase letters, digits, hyphens (-), and underscores (_). If the name is not specified, the original database name is used. |
      |                                   |                                                                                                                                                                                                                                                              |
      |                                   | .. note::                                                                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                                                              |
      |                                   |    -  The backup database can be renamed. A maximum of 100 backup databases can be created.                                                                                                                                                                  |
      |                                   |    -  The new database name cannot be the same as the name of any other database in the source.                                                                                                                                                              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Confirm Task** page, check configuration details, read and agree to the agreement, and click **Next**.

   .. note::

      If the SQL Server source contains non-clustered index tables, the index information of non-clustered index tables will become invalid after the SQL Server backups are restored to a new database. For the best performance, rebuild the indexes after the backup migration. In addition, the backup files store only database-level information. If the SQL Server source contains some instance-level configurations, such as login, permission, DBlink, and job, migrate these configurations by referring to :ref:`Manual Configuration <drs_04_0458>`

#. In the task list on the **Backup Migration Management** page, check whether the task is in the **Restoring** status. If the migration is successful, the task status becomes **Successful**.
