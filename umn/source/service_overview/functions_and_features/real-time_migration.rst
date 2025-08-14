:original_name: drs_01_0301.html

.. _drs_01_0301:

Real-Time Migration
===================

In real-time migration, you only need to configure the source database, destination database, and migration objects. DRS will help you compare and analyze data so you can determine when to migrate with minimal service disruption.

Supported Database Types
------------------------

DRS supports migration between different DB engines. The following table lists the supported data sources. Self-built databases include on-premises databases and ECS databases.

.. table:: **Table 1** Database types

   +--------------------------+---------------------------+-------------------------------+------------------------------+--------------------------------+
   | Migration Direction      | Data Flow                 | Source DB                     | Destination DB               | Destination DB Type            |
   +==========================+===========================+===============================+==============================+================================+
   | To the cloud             | MySQL->MySQL              | -  On-premises databases      | RDS for MySQL DB instances   | -  Single DB instance          |
   |                          |                           | -  ECS databases              |                              | -  Primary/Standby DB instance |
   |                          |                           | -  Databases on other clouds  |                              |                                |
   |                          |                           | -  RDS for MySQL DB instances |                              |                                |
   +--------------------------+---------------------------+-------------------------------+------------------------------+--------------------------------+
   | To the cloud             | MySQL -> TaurusDB Cluster | -  On-premises databases      | TaurusDB Cluster             | -  Primary/Standby DB instance |
   |                          |                           |                               |                              |                                |
   |                          |                           | -  ECS databases              |                              |                                |
   |                          |                           | -  Databases on other clouds  |                              |                                |
   |                          |                           | -  RDS for MySQL DB instances |                              |                                |
   |                          |                           | -  TaurusDB instances         |                              |                                |
   +--------------------------+---------------------------+-------------------------------+------------------------------+--------------------------------+
   | To the cloud             | MongoDB->DDS              | -  On-premises databases      | DDS DB instances             | -  Cluster                     |
   |                          |                           | -  ECS databases              |                              | -  Replica set                 |
   |                          |                           | -  Databases on other clouds  |                              | -  Single node                 |
   |                          |                           | -  DDS DB instances           |                              |                                |
   +--------------------------+---------------------------+-------------------------------+------------------------------+--------------------------------+
   | Out of the cloud         | MySQL->MySQL              | RDS for MySQL DB instances    | -  On-premises databases     | -  Single DB instance          |
   |                          |                           |                               | -  ECS databases             | -  Primary/Standby DB instance |
   |                          |                           |                               | -  Databases on other clouds |                                |
   +--------------------------+---------------------------+-------------------------------+------------------------------+--------------------------------+
   | Out of the cloud         | DDS->MongoDB              | DDS DB instances              | -  On-premises databases     | -  Cluster                     |
   |                          |                           |                               | -  ECS databases             | -  Replica set                 |
   |                          |                           |                               | -  Databases on other clouds | -  Single node                 |
   |                          |                           |                               | -  DDS instances             |                                |
   +--------------------------+---------------------------+-------------------------------+------------------------------+--------------------------------+
   | Self-built -> Self-built | MySQL->MySQL              | -  ECS databases              | -  ECS databases             | -  Single DB instance          |
   |                          |                           | -  On-premises databases      | -  On-premises databases     | -  Primary/Standby DB instance |
   +--------------------------+---------------------------+-------------------------------+------------------------------+--------------------------------+

.. table:: **Table 2** Database versions

   +--------------------------+---------------------------+-------------------+------------------------+
   | Migration Direction      | Data Flow                 | Source DB Version | Destination DB Version |
   +==========================+===========================+===================+========================+
   | To the cloud             | MySQL->MySQL              | -  MySQL 5.5.x    | -  MySQL 5.6.x         |
   |                          |                           | -  MySQL 5.6.x    | -  MySQL 5.7.x         |
   |                          |                           | -  MySQL 5.7.x    | -  MySQL 8.0.x         |
   |                          |                           | -  MySQL 8.0.x    |                        |
   +--------------------------+---------------------------+-------------------+------------------------+
   | To the cloud             | MongoDB->DDS              | -  MongoDB 3.2.x  | -  DDS 3.2.x           |
   |                          |                           | -  MongoDB 3.4.x  | -  DDS 3.4.x           |
   |                          |                           | -  MongoDB 3.6.x  | -  DDS 4.0.x           |
   |                          |                           | -  MongoDB 4.0.x  | -  DDS 4.2.x           |
   |                          |                           | -  MongoDB 4.2.x  | -  DDS 4.4.x           |
   |                          |                           | -  MongoDB 4.4.x  |                        |
   +--------------------------+---------------------------+-------------------+------------------------+
   | To the cloud             | MySQL -> TaurusDB Cluster | -  MySQL 5.6.x    | TaurusDB-MySQL 8.0     |
   |                          |                           | -  MySQL 5.7.x    |                        |
   |                          |                           | -  MySQL 8.0.x    |                        |
   +--------------------------+---------------------------+-------------------+------------------------+
   | Out of the cloud         | MySQL->MySQL              | -  MySQL 5.6.x    | -  MySQL 5.6.x         |
   |                          |                           | -  MySQL 5.7.x    | -  MySQL 5.7.x         |
   |                          |                           | -  MySQL 8.0.x    | -  MySQL 8.0.x         |
   +--------------------------+---------------------------+-------------------+------------------------+
   | Out of the cloud         | DDS->MongoDB              | -  DDS 3.2.x      | -  MongoDB 3.2.x       |
   |                          |                           | -  DDS 3.4.x      | -  MongoDB 3.4.x       |
   |                          |                           | -  DDS 4.0.x      | -  MongoDB 3.6.x       |
   |                          |                           | -  DDS 4.2.x      | -  MongoDB 4.0.x       |
   |                          |                           | -  DDS 4.4.x      | -  MongoDB 4.2.x       |
   |                          |                           |                   | -  MongoDB 4.4.x       |
   +--------------------------+---------------------------+-------------------+------------------------+
   | Self-built -> Self-built | MySQL->MySQL              | -  MySQL 5.5.x    | -  MySQL 5.6.x         |
   |                          |                           | -  MySQL 5.6.x    | -  MySQL 5.7.x         |
   |                          |                           | -  MySQL 5.7.x    | -  MySQL 8.0.x         |
   |                          |                           | -  MySQL 8.0.x    |                        |
   +--------------------------+---------------------------+-------------------+------------------------+

Supported Migration Types
-------------------------

DRS supports two migration types: full migration and full+incremental migration.

This full migration type is suitable for scenarios where service interruption is acceptable. All objects and data in non-system databases are migrated to the destination database at one time. The objects that can be migrated include tables, views, stored procedures, and triggers.

The full+incremental migration type allows you to migrate data without interrupting services. After a full migration initializes the destination database, an incremental migration parses logs to ensure data consistency between the source and destination databases.

.. table:: **Table 3** Migration types

   +--------------------------+---------------------------+-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | Migration Direction      | Data Flow                 | Full Migration                | Full+Incremental Migration                                                                                                                  |
   +==========================+===========================+===============================+=============================================================================================================================================+
   | To the cloud             | MySQL->MySQL              | Supported                     | Supported                                                                                                                                   |
   +--------------------------+---------------------------+-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | To the cloud             | MySQL -> TaurusDB Cluster | Supported                     | Supported                                                                                                                                   |
   +--------------------------+---------------------------+-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | To the cloud             | MongoDB->DDS              | -  Replica set -> Single node | -  Replica set -> Single node                                                                                                               |
   |                          |                           | -  Replica set -> Replica set | -  Replica set -> Replica set                                                                                                               |
   |                          |                           | -  Replica set -> Cluster     | -  Replica set -> Cluster                                                                                                                   |
   |                          |                           | -  Single node -> Single node | -  Single node -> Single node                                                                                                               |
   |                          |                           | -  Single node -> Replica set | -  Single node -> Replica set                                                                                                               |
   |                          |                           | -  Single node -> Cluster     | -  Single node -> Cluster                                                                                                                   |
   |                          |                           | -  Cluster -> Cluster         |                                                                                                                                             |
   |                          |                           |                               | .. note::                                                                                                                                   |
   |                          |                           |                               |                                                                                                                                             |
   |                          |                           |                               |    -  If you need to perform an incremental migration for a single-node instance, the source database must be the DDS single-node instance. |
   |                          |                           |                               |    -  The source cannot be a GaussDB(for Mongo) instance.                                                                                   |
   +--------------------------+---------------------------+-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | Out of the cloud         | MySQL->MySQL              | Supported                     | Supported                                                                                                                                   |
   +--------------------------+---------------------------+-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | Out of the cloud         | DDS->MongoDB              | Supported                     | Supported                                                                                                                                   |
   |                          |                           |                               |                                                                                                                                             |
   |                          |                           |                               | .. note::                                                                                                                                   |
   |                          |                           |                               |                                                                                                                                             |
   |                          |                           |                               |    If the source database is on a cluster instance, incremental migration is not supported.                                                 |
   +--------------------------+---------------------------+-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | Self-built -> Self-built | MySQL->MySQL              | Supported                     | Supported                                                                                                                                   |
   +--------------------------+---------------------------+-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+

Supported Network Types
-----------------------

DRS supports data migration through a Virtual Private Cloud (VPC), Virtual Private Network (VPN), Direct Connect, or public network. :ref:`Table 4 <drs_01_0301__en-us_topic_0000001205509269_en-us_topic_0000001147220024_en-us_topic_0000001102794420_table81301656181615>` lists the application scenarios of each network type and required preparations, and :ref:`Table 5 <drs_01_0301__en-us_topic_0000001205509269_en-us_topic_0000001147220024_en-us_topic_0000001102794420_table2942154915256>` lists the supported network types of each migration scenario.

.. _drs_01_0301__en-us_topic_0000001205509269_en-us_topic_0000001147220024_en-us_topic_0000001102794420_table81301656181615:

.. table:: **Table 4** Network types

   +-----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Network Type          | Application Scenario                                                                               | Preparations                                                                                                                                                                                                                                                                                                                                                       |
   +=======================+====================================================================================================+====================================================================================================================================================================================================================================================================================================================================================================+
   | VPC                   | Migrations between cloud databases in the same region                                              | -  The source and destination databases must be in the same region.                                                                                                                                                                                                                                                                                                |
   |                       |                                                                                                    | -  The source and destination databases can be in either the same VPC or in different VPCs.                                                                                                                                                                                                                                                                        |
   |                       |                                                                                                    | -  If source and destination databases are in the same VPC, they can communicate with each other by default. Therefore, you do not need to configure a security group.                                                                                                                                                                                             |
   |                       |                                                                                                    | -  If the source and destination databases are not in the same VPC, the CIDR blocks of the source and destination databases cannot be duplicated or overlapped, and the source and destination databases are connected through a VPC peering connection. DRS automatically establishes a route through a single IP address when you test the network connectivity. |
   +-----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VPN                   | Migrations from on-premises databases to cloud databases or between cloud databases across regions | Establish a VPN connection between your local data center and the VPC that hosts the destination database. Before migration, ensure that the VPN network is accessible.                                                                                                                                                                                            |
   +-----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Direct Connect        | Migrations from on-premises databases to cloud databases or between cloud databases across regions | Use a dedicated network connection to connect your data center to VPCs.                                                                                                                                                                                                                                                                                            |
   +-----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Public network        | Migrations from on-premises or other cloud databases to destination databases                      | To ensure network connectivity between the source and destination databases, perform the following operations:                                                                                                                                                                                                                                                     |
   |                       |                                                                                                    |                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                    | #. Enable public accessibility.                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                    |                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                    |    Enable public accessibility for the source database based on your service requirements.                                                                                                                                                                                                                                                                         |
   |                       |                                                                                                    |                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                    | #. Configure security group rules.                                                                                                                                                                                                                                                                                                                                 |
   |                       |                                                                                                    |                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                    |    -  Add the EIPs of the replication instance to the whitelist of the source database for inbound traffic.                                                                                                                                                                                                                                                        |
   |                       |                                                                                                    |    -  If destination databases and the replication instance are in the same VPC, they can communicate with each other by default. You do not need to configure a security group.                                                                                                                                                                                   |
   |                       |                                                                                                    |                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                    |    .. note::                                                                                                                                                                                                                                                                                                                                                       |
   |                       |                                                                                                    |                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                                                                                                    |       -  The IP address on the **Configure Source and Destination Databases** page is the EIP of the replication instance.                                                                                                                                                                                                                                         |
   |                       |                                                                                                    |       -  If SSL is not enabled, migrating confidential data is not recommended.                                                                                                                                                                                                                                                                                    |
   +-----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _drs_01_0301__en-us_topic_0000001205509269_en-us_topic_0000001147220024_en-us_topic_0000001102794420_table2942154915256:

.. table:: **Table 5** Supported network types

   +--------------------------+---------------------------+---------------+----------------+-----------------------+
   | Migration Direction      | Data Flow                 | VPC           | Public Network | VPN or Direct Connect |
   +==========================+===========================+===============+================+=======================+
   | To the cloud             | MySQL->MySQL              | Supported     | Supported      | Supported             |
   +--------------------------+---------------------------+---------------+----------------+-----------------------+
   | To the cloud             | MySQL -> TaurusDB Cluster | Supported     | Supported      | Supported             |
   +--------------------------+---------------------------+---------------+----------------+-----------------------+
   | To the cloud             | MongoDB->DDS              | Supported     | Supported      | Supported             |
   +--------------------------+---------------------------+---------------+----------------+-----------------------+
   | Out of the cloud         | MySQL->MySQL              | Supported     | Supported      | Supported             |
   +--------------------------+---------------------------+---------------+----------------+-----------------------+
   | Out of the cloud         | DDS->MongoDB              | Supported     | Supported      | Supported             |
   +--------------------------+---------------------------+---------------+----------------+-----------------------+
   | Self-built -> Self-built | MySQL->MySQL              | Not supported | Supported      | Supported             |
   +--------------------------+---------------------------+---------------+----------------+-----------------------+

Migration Objects
-----------------

DRS allows you to migrate objects at different levels. The following table lists the supported migration objects.

.. table:: **Table 6** Supported migration objects

   +--------------------------+---------------------------+----------------+-----------------------+--------------------------+
   | Migration Direction      | Data Flow                 | Full Migration | Table-Level Migration | Database-Level Migration |
   +==========================+===========================+================+=======================+==========================+
   | To the cloud             | MySQL->MySQL              | Supported      | Supported             | Supported                |
   +--------------------------+---------------------------+----------------+-----------------------+--------------------------+
   | To the cloud             | MySQL -> TaurusDB Cluster | Supported      | Supported             | Supported                |
   +--------------------------+---------------------------+----------------+-----------------------+--------------------------+
   | To the cloud             | MongoDB->DDS              | Supported      | Supported             | Supported                |
   +--------------------------+---------------------------+----------------+-----------------------+--------------------------+
   | Out of the cloud         | MySQL->MySQL              | Supported      | Supported             | Supported                |
   +--------------------------+---------------------------+----------------+-----------------------+--------------------------+
   | Out of the cloud         | DDS->MongoDB              | Supported      | Supported             | Supported                |
   +--------------------------+---------------------------+----------------+-----------------------+--------------------------+
   | Self-built -> Self-built | MySQL->MySQL              | Supported      | Supported             | Supported                |
   +--------------------------+---------------------------+----------------+-----------------------+--------------------------+

Advanced Features
-----------------

DRS supports multiple features to ensure successful real-time migration.

.. table:: **Table 7** Advanced features

   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Feature                           | Description                                                                                                                                                              |
   +===================================+==========================================================================================================================================================================+
   | Flow control                      | Allows you to limit the overall migration speed to make the impact of migration on bandwidth and database I/O controllable.                                              |
   |                                   |                                                                                                                                                                          |
   |                                   | Flow control mode takes effect only during a full migration.                                                                                                             |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Account migration                 | Allows you to migrate accounts, permissions, and passwords.                                                                                                              |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter comparison              | Checks the consistency of common parameters and performance parameters between source and destination databases to ensure that the migrated service is running properly. |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
