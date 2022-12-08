:original_name: drs_01_0303.html

.. _drs_01_0303:

Backup Migration
================

DRS supports backup migrations of various database types.

Supported Database Types
------------------------

.. table:: **Table 1** Database types

   +--------------------------------------------------+------------------------------------------------------+---------------------------------------+
   | Data Flow                                        | Backup File Source                                   | Destination DB Type                   |
   +==================================================+======================================================+=======================================+
   | Microsoft SQL Server -> RDS Microsoft SQL Server | -  On-premises Microsoft SQL Server backup files     | RDS Microsoft SQL Server DB instances |
   |                                                  | -  RDS Microsoft SQL Server full backup files        |                                       |
   |                                                  | -  Microsoft SQL Server backup files on other clouds |                                       |
   +--------------------------------------------------+------------------------------------------------------+---------------------------------------+

Migration Methods
-----------------

.. table:: **Table 2** Migration methods

   +--------------------------------------------------+----------------+-----------------------+
   | Data Flow                                        | Full Migration | Incremental Migration |
   +==================================================+================+=======================+
   | Microsoft SQL Server -> RDS Microsoft SQL Server | Supported      | Supported             |
   +--------------------------------------------------+----------------+-----------------------+

Supported Database Versions
---------------------------

.. table:: **Table 3** Database versions

   +--------------------------------------------------+--------------------------------------------------------------------------+------------------------------+
   | Data Flow                                        | Backup File Version                                                      | Destination DB Version       |
   +==================================================+==========================================================================+==============================+
   | Microsoft SQL Server -> RDS Microsoft SQL Server | On-premises and other cloud's Microsoft SQL Server backup file versions: | -  Microsoft SQL Server 2008 |
   |                                                  |                                                                          | -  Microsoft SQL Server 2012 |
   |                                                  | -  Microsoft SQL Server 2000                                             | -  Microsoft SQL Server 2014 |
   |                                                  | -  Microsoft SQL Server 2005                                             | -  Microsoft SQL Server 2016 |
   |                                                  | -  Microsoft SQL Server 2008                                             | -  Microsoft SQL Server 2017 |
   |                                                  | -  Microsoft SQL Server 2012                                             | -  Microsoft SQL Server 2019 |
   |                                                  | -  Microsoft SQL Server 2014                                             |                              |
   |                                                  | -  Microsoft SQL Server 2016                                             |                              |
   |                                                  | -  Microsoft SQL Server 2017                                             |                              |
   |                                                  | -  Microsoft SQL Server 2019                                             |                              |
   +--------------------------------------------------+--------------------------------------------------------------------------+------------------------------+
   |                                                  | RDS Microsoft SQL Server full backup file versions:                      | -  Microsoft SQL Server 2008 |
   |                                                  |                                                                          | -  Microsoft SQL Server 2012 |
   |                                                  | -  Microsoft SQL Server 2008                                             | -  Microsoft SQL Server 2014 |
   |                                                  | -  Microsoft SQL Server 2012                                             | -  Microsoft SQL Server 2016 |
   |                                                  | -  Microsoft SQL Server 2014                                             | -  Microsoft SQL Server 2017 |
   |                                                  | -  Microsoft SQL Server 2016                                             | -  Microsoft SQL Server 2019 |
   |                                                  | -  Microsoft SQL Server 2017                                             |                              |
   |                                                  | -  Microsoft SQL Server 2019                                             |                              |
   +--------------------------------------------------+--------------------------------------------------------------------------+------------------------------+

Backup Migration Scenarios
--------------------------

.. table:: **Table 4** Migration scenarios

   +-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Scenario        | Description                                                                                                                                                            |
   +=================+========================================================================================================================================================================+
   | OBS bucket      | If you copy the database backup files to an Object Storage Service (OBS) bucket, ensure that the OBS bucket is located in the same region as the destination instance. |
   +-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RDS full backup | If you select an RDS full backup as the backup file source, ensure that the RDS instance has a full backup.                                                            |
   +-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
