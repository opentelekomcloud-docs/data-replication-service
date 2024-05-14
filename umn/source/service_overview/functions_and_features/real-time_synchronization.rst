:original_name: drs_01_0302.html

.. _drs_01_0302:

Real-Time Synchronization
=========================

Real-time synchronization refers to the real-time flow of key service data from sources to destinations while consistency of data can be ensured. It is different from migration. Migration means moving your overall database from one platform to another. Synchronization refers to the continuous flow of data between different services.

Supported Database Types
------------------------

DRS supports real-time synchronization between databases of various types, and many-to-one synchronization.

.. table:: **Table 1** Database types

   +---------------------------+---------------------------------------------+--------------------------------+------------------------------------+--------------------------------+
   | Synchronization Direction | Data Flow                                   | Source DB                      | Destination DB                     | Destination DB Type            |
   +===========================+=============================================+================================+====================================+================================+
   | To the cloud              | MySQL->MySQL                                | -  On-premises databases       | RDS MySQL DB instances             | -  Single DB instance          |
   |                           |                                             | -  ECS databases               |                                    | -  Primary/Standby DB instance |
   |                           |                                             | -  Databases on other clouds   |                                    |                                |
   |                           |                                             | -  RDS MySQL DB instances      |                                    |                                |
   +---------------------------+---------------------------------------------+--------------------------------+------------------------------------+--------------------------------+
   | To the cloud              | MySQL-> GaussDB distributed                 | -  On-premises databases       | GaussDB distributed                | -  Cluster                     |
   |                           |                                             | -  ECS databases               |                                    |                                |
   |                           |                                             | -  Databases on other clouds   |                                    |                                |
   |                           |                                             | -  RDS MySQL DB instances      |                                    |                                |
   +---------------------------+---------------------------------------------+--------------------------------+------------------------------------+--------------------------------+
   | To the cloud              | MySQL -> GaussDB(for MySQL) primary/standby | -  On-premises databases       | GaussDB(for MySQL) primary/standby | -  Primary/Standby DB instance |
   |                           |                                             | -  ECS databases               |                                    |                                |
   |                           |                                             | -  Databases on other clouds   |                                    |                                |
   |                           |                                             | -  RDS MySQL DB instances      |                                    |                                |
   +---------------------------+---------------------------------------------+--------------------------------+------------------------------------+--------------------------------+
   | To the cloud              | PostgreSQL->PostgreSQL                      | -  On-premises databases       | RDS PostgreSQL DB instances        | -  Single DB instance          |
   |                           |                                             | -  ECS databases               |                                    | -  Primary/Standby DB instance |
   |                           |                                             | -  Databases on other clouds   |                                    |                                |
   |                           |                                             | -  RDS PostgreSQL DB instances |                                    |                                |
   +---------------------------+---------------------------------------------+--------------------------------+------------------------------------+--------------------------------+
   | To the cloud              | Oracle->PostgreSQL                          | -  On-premises databases       | RDS PostgreSQL DB instances        | -  Single DB instance          |
   |                           |                                             | -  ECS databases               |                                    | -  Primary/Standby DB instance |
   +---------------------------+---------------------------------------------+--------------------------------+------------------------------------+--------------------------------+
   | From the cloud            | MySQL->MySQL                                | RDS MySQL DB instances         | -  On-premises databases           | ``-``                          |
   |                           |                                             |                                | -  ECS databases                   |                                |
   |                           |                                             |                                | -  Databases on other clouds       |                                |
   |                           |                                             |                                | -  RDS MySQL DB instances          |                                |
   +---------------------------+---------------------------------------------+--------------------------------+------------------------------------+--------------------------------+
   | From the cloud            | MySQL->Kafka                                | RDS MySQL DB instances         | -  Kafka                           | -  Cluster                     |
   |                           |                                             |                                | -  DMS for Kafka                   | -  Single node                 |
   +---------------------------+---------------------------------------------+--------------------------------+------------------------------------+--------------------------------+
   | From the cloud            | GaussDB distributed -> MySQL                | GaussDB distributed            | -  On-premises databases           | ``-``                          |
   |                           |                                             |                                | -  ECS databases                   |                                |
   |                           |                                             |                                | -  Databases on other clouds       |                                |
   |                           |                                             |                                | -  RDS MySQL instances             |                                |
   +---------------------------+---------------------------------------------+--------------------------------+------------------------------------+--------------------------------+
   | Self-built -> Self-built  | MySQL->MySQL                                | -  On-premises databases       | -  On-premises databases           | -  Single DB instance          |
   |                           |                                             | -  ECS databases               | -  ECS databases                   | -  Primary/Standby DB instance |
   +---------------------------+---------------------------------------------+--------------------------------+------------------------------------+--------------------------------+
   | Self-built -> Self-built  | MySQL->Kafka                                | -  On-premises databases       | -  Kafka                           | -  Cluster                     |
   |                           |                                             | -  ECS databases               | -  DMS for Kafka                   | -  Single node                 |
   +---------------------------+---------------------------------------------+--------------------------------+------------------------------------+--------------------------------+

Synchronization Methods
-----------------------

DRS supports three synchronization modes: full synchronization, incremental synchronization, and full+incremental synchronization.

Full synchronization: All objects and data in non-system databases are synchronized to the destination database at a time. This mode is applicable to scenarios where service interruption is acceptable.

Incremental synchronization: Through log parsing, DRS replicates incremental data to keep sources and destinations in sync.

Full+Incremental synchronization: DRS allows you to synchronize data in real time. After a full synchronization initializes the destination database, an incremental synchronization parses logs to ensure data consistency between the source and destination databases.

.. table:: **Table 2** Synchronization methods

   +---------------------------+---------------------------------------------+---------------+---------------+------------------+----------------------+
   | Synchronization Direction | Data Flow                                   | Incremental   | Full          | Full+Incremental | One-way/Two-way Sync |
   +===========================+=============================================+===============+===============+==================+======================+
   | To the cloud              | MySQL->MySQL                                | Supported     | Not supported | Supported        | One-way sync         |
   +---------------------------+---------------------------------------------+---------------+---------------+------------------+----------------------+
   | To the cloud              | MySQL-> GaussDB distributed                 | Not supported | Not supported | Supported        | One-way sync         |
   +---------------------------+---------------------------------------------+---------------+---------------+------------------+----------------------+
   | To the cloud              | MySQL -> GaussDB(for MySQL) primary/standby | Supported     | Not supported | Supported        | One-way sync         |
   +---------------------------+---------------------------------------------+---------------+---------------+------------------+----------------------+
   | To the cloud              | PostgreSQL->PostgreSQL                      | Supported     | Supported     | Supported        | One-way sync         |
   +---------------------------+---------------------------------------------+---------------+---------------+------------------+----------------------+
   | To the cloud              | Oracle->PostgreSQL                          | Not supported | Supported     | Supported        | One-way sync         |
   +---------------------------+---------------------------------------------+---------------+---------------+------------------+----------------------+
   | From the cloud            | MySQL->MySQL                                | Supported     | Not supported | Supported        | One-way sync         |
   +---------------------------+---------------------------------------------+---------------+---------------+------------------+----------------------+
   | From the cloud            | MySQL->Kafka                                | Supported     | Not supported | Not supported    | One-way sync         |
   +---------------------------+---------------------------------------------+---------------+---------------+------------------+----------------------+
   | From the cloud            | GaussDB distributed -> MySQL                | Supported     | Not supported | Not supported    | One-way sync         |
   +---------------------------+---------------------------------------------+---------------+---------------+------------------+----------------------+
   | Self-built -> Self-built  | MySQL->MySQL                                | Supported     | Not supported | Supported        | One-way sync         |
   +---------------------------+---------------------------------------------+---------------+---------------+------------------+----------------------+
   | Self-built -> Self-built  | MySQL->Kafka                                | Supported     | Not supported | Not supported    | One-way sync         |
   +---------------------------+---------------------------------------------+---------------+---------------+------------------+----------------------+

Database Versions
-----------------

.. note::

   Data cannot be synchronized from a newer version database to an older version database.

.. table:: **Table 3** Database versions

   +---------------------------+---------------------------------------------+-------------------------+------------------------------+
   | Synchronization Direction | Data Flow                                   | Source Database Version | Destination DB Version       |
   +===========================+=============================================+=========================+==============================+
   | To the cloud              | MySQL->MySQL                                | -  MySQL 5.5.x          | -  MySQL 5.6.x               |
   |                           |                                             | -  MySQL 5.6.x          | -  MySQL 5.7.x               |
   |                           |                                             | -  MySQL 5.7.x          | -  MySQL 8.0.x               |
   |                           |                                             | -  MySQL 8.0.x          |                              |
   +---------------------------+---------------------------------------------+-------------------------+------------------------------+
   | To the cloud              | MySQL-> GaussDB distributed                 | -  MySQL 5.5.x          | -  GaussDB 1.0.0 or later    |
   |                           |                                             | -  MySQL 5.6.x          |                              |
   |                           |                                             | -  MySQL 5.7.x          |                              |
   +---------------------------+---------------------------------------------+-------------------------+------------------------------+
   | To the cloud              | MySQL -> GaussDB(for MySQL) primary/standby | -  MySQL 5.5.x          | GaussDB(for MySQL)-MySQL 8.0 |
   |                           |                                             | -  MySQL 5.6.x          |                              |
   |                           |                                             | -  MySQL 5.7.x          |                              |
   |                           |                                             | -  MySQL 8.0.x          |                              |
   +---------------------------+---------------------------------------------+-------------------------+------------------------------+
   | To the cloud              | PostgreSQL->PostgreSQL                      | -  PostgreSQL 9.4.x     | -  PostgreSQL 9.5.x          |
   |                           |                                             | -  PostgreSQL 9.5.x     | -  PostgreSQL 9.6.x          |
   |                           |                                             | -  PostgreSQL 9.6.x     | -  PostgreSQL 10.x           |
   |                           |                                             | -  PostgreSQL 10.x      | -  PostgreSQL 11.x           |
   |                           |                                             | -  PostgreSQL 11.x      | -  PostgreSQL 12.x           |
   |                           |                                             | -  PostgreSQL 12.x      | -  PostgreSQL 13.x           |
   |                           |                                             | -  PostgreSQL 13.x      | -  PostgreSQL 14.x           |
   |                           |                                             | -  PostgreSQL 14.x      |                              |
   +---------------------------+---------------------------------------------+-------------------------+------------------------------+
   | To the cloud              | Oracle->PostgreSQL                          | -  Oracle 10g           | -  PostgreSQL 9.5.x          |
   |                           |                                             | -  Oracle 11g           | -  PostgreSQL 9.6.x          |
   |                           |                                             | -  Oracle 12c           | -  PostgreSQL 10.x           |
   |                           |                                             | -  Oracle 18c           | -  PostgreSQL 11.x           |
   |                           |                                             | -  Oracle 19c           | -  PostgreSQL 12.x           |
   |                           |                                             | -  Oracle 21c           | -  PostgreSQL 13.x           |
   |                           |                                             |                         | -  PostgreSQL 14.x           |
   +---------------------------+---------------------------------------------+-------------------------+------------------------------+
   | From the cloud            | MySQL->MySQL                                | -  MySQL 5.6.x          | -  MySQL 5.6.x               |
   |                           |                                             | -  MySQL 5.7.x          | -  MySQL 5.7.x               |
   |                           |                                             | -  MySQL 8.0.x          | -  MySQL 8.0.x               |
   +---------------------------+---------------------------------------------+-------------------------+------------------------------+
   | From the cloud            | MySQL->Kafka                                | -  MySQL 5.6.x          | Kafka 0.11 or later          |
   |                           |                                             | -  MySQL 5.7.x          |                              |
   +---------------------------+---------------------------------------------+-------------------------+------------------------------+
   | From the cloud            | GaussDB distributed -> MySQL                | GaussDB 1.3             | -  MySQL 5.5.x               |
   |                           |                                             |                         | -  MySQL 5.6.x               |
   |                           |                                             |                         | -  MySQL 5.7.x               |
   +---------------------------+---------------------------------------------+-------------------------+------------------------------+
   | Self-built -> Self-built  | MySQL->MySQL                                | -  MySQL 5.5.x          | -  MySQL 5.6.x               |
   |                           |                                             | -  MySQL 5.6.x          | -  MySQL 5.7.x               |
   |                           |                                             | -  MySQL 5.7.x          | -  MySQL 8.0.x               |
   |                           |                                             | -  MySQL 8.0.x          |                              |
   +---------------------------+---------------------------------------------+-------------------------+------------------------------+
   | Self-built -> Self-built  | MySQL->Kafka                                | -  MySQL 5.5.x          | Kafka 0.11 or later          |
   |                           |                                             | -  MySQL 5.6.x          |                              |
   |                           |                                             | -  MySQL 5.7.x          |                              |
   |                           |                                             | -  MySQL 8.0.x          |                              |
   +---------------------------+---------------------------------------------+-------------------------+------------------------------+

Network Types
-------------

DRS supports real-time synchronization through a Virtual Private Cloud (VPC), Virtual Private Network (VPN), Direct Connect, or public network. :ref:`Table 4 <drs_01_0302__en-us_topic_0000001205627793_en-us_topic_0000001193299771_en-us_topic_0000001149354299_table81301656181615>` lists the application scenarios of each network type and required preparations.

.. _drs_01_0302__en-us_topic_0000001205627793_en-us_topic_0000001193299771_en-us_topic_0000001149354299_table81301656181615:

.. table:: **Table 4** Network types

   +-----------------------+---------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Network Type          | Application Scenario                                                                                    | Preparations                                                                                                                                                                                                                                                                                                                                                       |
   +=======================+=========================================================================================================+====================================================================================================================================================================================================================================================================================================================================================================+
   | VPC                   | Synchronization between cloud databases in the same region                                              | -  The source and destination databases must be in the same region.                                                                                                                                                                                                                                                                                                |
   |                       |                                                                                                         | -  The source and destination databases can be in either the same VPC or in different VPCs.                                                                                                                                                                                                                                                                        |
   |                       |                                                                                                         | -  If source and destination databases are in the same VPC, they can communicate with each other by default. Therefore, you do not need to configure a security group.                                                                                                                                                                                             |
   |                       |                                                                                                         | -  If the source and destination databases are not in the same VPC, the CIDR blocks of the source and destination databases cannot be duplicated or overlapped, and the source and destination databases are connected through a VPC peering connection. DRS automatically establishes a route through a single IP address when you test the network connectivity. |
   +-----------------------+---------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VPN                   | Synchronization from on-premises databases to cloud databases or between cloud databases across regions | Establish a VPN connection between your local data center and the VPC that hosts the destination database. Before synchronization, ensure that the VPN network is accessible.                                                                                                                                                                                      |
   +-----------------------+---------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Direct Connect        | Synchronization from on-premises databases to cloud databases or between cloud databases across regions | Use a dedicated network connection to connect your data center to VPCs.                                                                                                                                                                                                                                                                                            |
   +-----------------------+---------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Public network        | Synchronization from on-premises or external cloud databases to the destination databases.              | To ensure network connectivity between the source and destination databases, perform the following operations:                                                                                                                                                                                                                                                     |
   |                       |                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                         | #. Enable public accessibility.                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                         |    Enable public accessibility for the source database based on your service requirements.                                                                                                                                                                                                                                                                         |
   |                       |                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                         | #. Configure security group rules.                                                                                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                         |    -  Add the EIPs of the synchronization instance to the whitelist of the source database for inbound traffic.                                                                                                                                                                                                                                                    |
   |                       |                                                                                                         |    -  If destination databases and the synchronization instance are in the same VPC, they can communicate with each other by default. Therefore, you do not need to configure a security group.                                                                                                                                                                    |
   |                       |                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                         |    .. note::                                                                                                                                                                                                                                                                                                                                                       |
   |                       |                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                         |       -  The IP address on the **Configure Source and Destination Databases** page is the EIP of the synchronization instance.                                                                                                                                                                                                                                     |
   |                       |                                                                                                         |       -  If SSL is not enabled, synchronizing confidential data is not recommended.                                                                                                                                                                                                                                                                                |
   +-----------------------+---------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 5** Supported network types

   +---------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | Synchronization Direction | Data Flow                                   | VPC           | Public Network | VPN or Direct Connect |
   +===========================+=============================================+===============+================+=======================+
   | To the cloud              | MySQL->MySQL                                | Supported     | Supported      | Supported             |
   +---------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | To the cloud              | MySQL-> GaussDB distributed                 | Supported     | Supported      | Supported             |
   +---------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | To the cloud              | MySQL -> GaussDB(for MySQL) primary/standby | Supported     | Supported      | Supported             |
   +---------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | To the cloud              | PostgreSQL->PostgreSQL                      | Supported     | Supported      | Supported             |
   +---------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | To the cloud              | Oracle->PostgreSQL                          | Supported     | Supported      | Supported             |
   +---------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | From the cloud            | MySQL->MySQL                                | Supported     | Supported      | Supported             |
   +---------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | From the cloud            | MySQL->Kafka                                | Supported     | Supported      | Supported             |
   +---------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | From the cloud            | GaussDB distributed -> MySQL                | Not supported | Supported      | Supported             |
   +---------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | Self-built -> Self-built  | MySQL->MySQL                                | Not supported | Supported      | Supported             |
   +---------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | Self-built -> Self-built  | MySQL->Kafka                                | Supported     | Supported      | Supported             |
   +---------------------------+---------------------------------------------+---------------+----------------+-----------------------+

Supported Synchronization Objects
---------------------------------

DRS allows you to synchronize different objects. The following table lists the supported objects.

.. table:: **Table 6** Supported synchronization objects

   +---------------------------+---------------------------------------------+-------------+----------------+--------------------------+
   | Synchronization Direction | Data Flow                                   | Table-level | Database-level | Importing an Object File |
   +===========================+=============================================+=============+================+==========================+
   | To the cloud              | MySQL->MySQL                                | Supported   | Supported      | Supported                |
   +---------------------------+---------------------------------------------+-------------+----------------+--------------------------+
   | To the cloud              | MySQL-> GaussDB distributed                 | Supported   | Not supported  | Not supported            |
   +---------------------------+---------------------------------------------+-------------+----------------+--------------------------+
   | To the cloud              | MySQL -> GaussDB(for MySQL) primary/standby | Supported   | Supported      | Supported                |
   +---------------------------+---------------------------------------------+-------------+----------------+--------------------------+
   | To the cloud              | PostgreSQL->PostgreSQL                      | Supported   | Supported      | Supported                |
   +---------------------------+---------------------------------------------+-------------+----------------+--------------------------+
   | To the cloud              | Oracle->PostgreSQL                          | Supported   | Not supported  | Supported                |
   +---------------------------+---------------------------------------------+-------------+----------------+--------------------------+
   | From the cloud            | MySQL->MySQL                                | Supported   | Supported      | Not supported            |
   +---------------------------+---------------------------------------------+-------------+----------------+--------------------------+
   | From the cloud            | MySQL->Kafka                                | Supported   | Supported      | Supported                |
   +---------------------------+---------------------------------------------+-------------+----------------+--------------------------+
   | From the cloud            | GaussDB distributed -> MySQL                | Supported   | Not supported  | Not supported            |
   +---------------------------+---------------------------------------------+-------------+----------------+--------------------------+
   | Self-built -> Self-built  | MySQL->MySQL                                | Supported   | Supported      | Not supported            |
   +---------------------------+---------------------------------------------+-------------+----------------+--------------------------+
   | Self-built -> Self-built  | MySQL->Kafka                                | Supported   | Supported      | Supported                |
   +---------------------------+---------------------------------------------+-------------+----------------+--------------------------+

Advanced Features
-----------------

DRS supports multiple features to ensure successful data synchronization.

.. table:: **Table 7** Advanced features

   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Feature                                                | Description                                                                                                                                                                                                                                                                                                                                |
   +========================================================+============================================================================================================================================================================================================================================================================================================================================+
   | Synchronization level                                  | DRS supports database- and table-level synchronization.                                                                                                                                                                                                                                                                                    |
   |                                                        |                                                                                                                                                                                                                                                                                                                                            |
   |                                                        | -  Database-level synchronization refers to a type of synchronization method using database as a unit. You do not need to select tables to be synchronized. New tables in the database are automatically added to the synchronization task.                                                                                                |
   |                                                        | -  Table-level synchronization uses table as a unit, indicating that you need to add new tables to the synchronization task manually.                                                                                                                                                                                                      |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Mapping object names                                   | Allows the names of synchronization objects (including databases, schemas, tables, and columns) in the source database to be different from those in the destination database. If the synchronization objects in source and destination databases have different names, you can map the source object name to the destination one.         |
   |                                                        |                                                                                                                                                                                                                                                                                                                                            |
   |                                                        | The following objects can be mapped: databases, schemas and tables.                                                                                                                                                                                                                                                                        |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Dynamically adding or deleting synchronization objects | During data synchronization, you can add or delete synchronization objects as required.                                                                                                                                                                                                                                                    |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Conflict policy                                        | DRS uses primary key or unique key conflict policies to ensure that tables with primary key or unique constraints in the source database can be synchronized to the destination database as expected.                                                                                                                                      |
   |                                                        |                                                                                                                                                                                                                                                                                                                                            |
   |                                                        | The following conflict policies are supported:                                                                                                                                                                                                                                                                                             |
   |                                                        |                                                                                                                                                                                                                                                                                                                                            |
   |                                                        | -  Ignore                                                                                                                                                                                                                                                                                                                                  |
   |                                                        |                                                                                                                                                                                                                                                                                                                                            |
   |                                                        |    The system will skip the conflicting data and continue the subsequent synchronization process.                                                                                                                                                                                                                                          |
   |                                                        |                                                                                                                                                                                                                                                                                                                                            |
   |                                                        | -  Overwrite                                                                                                                                                                                                                                                                                                                               |
   |                                                        |                                                                                                                                                                                                                                                                                                                                            |
   |                                                        |    Conflicting data will be overwritten.                                                                                                                                                                                                                                                                                                   |
   |                                                        |                                                                                                                                                                                                                                                                                                                                            |
   |                                                        | -  Report error                                                                                                                                                                                                                                                                                                                            |
   |                                                        |                                                                                                                                                                                                                                                                                                                                            |
   |                                                        |    The synchronization task will be stopped and fail.                                                                                                                                                                                                                                                                                      |
   |                                                        |                                                                                                                                                                                                                                                                                                                                            |
   |                                                        | Ignore and overwrite: Synchronization stability is prioritized, so tasks will not be interrupted as data conflicts occur.                                                                                                                                                                                                                  |
   |                                                        |                                                                                                                                                                                                                                                                                                                                            |
   |                                                        | Report error: Data quality is prioritized. Any data conflicts are not allowed, so once a conflict occurs, the synchronization task fails and an error is reported. You need to manually find the cause of the fault. If the task is in the failed state for a long time, the storage space may be used up and the task cannot be restored. |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Structure synchronization                              | DRS does not provide data structure synchronization as an independent function during real-time synchronization. Instead, it directly synchronizes data and structures to the destination database.                                                                                                                                        |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
