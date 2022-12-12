:original_name: drs_01_0305.html

.. _drs_01_0305:

Real-Time Disaster Recovery
===========================

Database Types
--------------

DRS supports disaster recovery (DR) management for the following types of databases.

.. table:: **Table 1** Database types

   +--------------------------+---------------------------------------------+-------------------------------------+----------------------------------------------+--------------------------------+
   | DR Direction             | Data Flow                                   | Service Database                    | DR Database                                  | DR DB Instance Type            |
   +==========================+=============================================+=====================================+==============================================+================================+
   | Current cloud as standby | MySQL->MySQL                                | -  On-premises databases            | RDS MySQL instances                          | -  Single DB instance          |
   |                          |                                             | -  Databases on an ECS              |                                              | -  Primary/Standby DB instance |
   |                          |                                             | -  Databases on other clouds        |                                              |                                |
   |                          |                                             | -  RDS MySQL instances              |                                              |                                |
   +--------------------------+---------------------------------------------+-------------------------------------+----------------------------------------------+--------------------------------+
   | Current cloud as active  | MySQL->MySQL                                | RDS MySQL instances                 | -  On-premises databases                     | -  Single DB instance          |
   |                          |                                             |                                     | -  ECS databases                             | -  Primary/Standby DB instance |
   |                          |                                             |                                     | -  Databases on other clouds                 |                                |
   |                          |                                             |                                     | -  RDS MySQL instances                       |                                |
   +--------------------------+---------------------------------------------+-------------------------------------+----------------------------------------------+--------------------------------+
   | Current cloud as standby | MySQL -> GaussDB(for MySQL) primary/standby | -  On-premises databases            | GaussDB(for MySQL) primary/standby instances | -  Primary/Standby instance    |
   |                          |                                             | -  ECS databases                    |                                              |                                |
   |                          |                                             | -  Databases on other clouds        |                                              |                                |
   |                          |                                             | -  RDS MySQL instances              |                                              |                                |
   +--------------------------+---------------------------------------------+-------------------------------------+----------------------------------------------+--------------------------------+
   | Current cloud as standby | Cassandra->Cassandra                        | -  On-premises databases            | GaussDB(for Cassandra) instances             | -  Cluster                     |
   |                          |                                             | -  ECS databases                    |                                              |                                |
   |                          |                                             | -  Databases on other clouds        |                                              |                                |
   |                          |                                             | -  GaussDB(for Cassandra) instances |                                              |                                |
   +--------------------------+---------------------------------------------+-------------------------------------+----------------------------------------------+--------------------------------+
   | Current cloud as active  | Cassandra->Cassandra                        | -  GaussDB(for Cassandra)           | -  On-premises databases                     | -  Cluster                     |
   |                          |                                             |                                     | -  ECS databases                             |                                |
   |                          |                                             |                                     | -  Databases on other clouds                 |                                |
   |                          |                                             |                                     | -  GaussDB(for Cassandra) instances          |                                |
   +--------------------------+---------------------------------------------+-------------------------------------+----------------------------------------------+--------------------------------+

Database Versions
-----------------

.. table:: **Table 2** Database versions

   +--------------------------+---------------------------------------------+----------------------------+------------------------------+
   | DR Direction             | Data Flow                                   | Service Database Version   | DR Database Version          |
   +==========================+=============================================+============================+==============================+
   | Current cloud as standby | MySQL->MySQL                                | -  MySQL 5.6.x             | -  MySQL 5.6.x               |
   |                          |                                             | -  MySQL 5.7.x             | -  MySQL 5.7.x               |
   |                          |                                             | -  MySQL 8.0.x             | -  MySQL 8.0.x               |
   +--------------------------+---------------------------------------------+----------------------------+------------------------------+
   | Current cloud as active  | MySQL->MySQL                                | -  MySQL 5.6.x             | -  MySQL 5.6.x               |
   |                          |                                             | -  MySQL 5.7.x             | -  MySQL 5.7.x               |
   |                          |                                             | -  MySQL 8.0.x             | -  MySQL 8.0.x               |
   +--------------------------+---------------------------------------------+----------------------------+------------------------------+
   | Current cloud as standby | MySQL -> GaussDB(for MySQL) primary/standby | -  MySQL 5.6.x             | GaussDB(for MySQL)-MySQL 8.0 |
   |                          |                                             | -  MySQL 5.7.x             |                              |
   +--------------------------+---------------------------------------------+----------------------------+------------------------------+
   | Current cloud as standby | Cassandra-> Cassandra                       | Cassandra 2.x              | GaussDB(for Cassandra) 3.x   |
   +--------------------------+---------------------------------------------+----------------------------+------------------------------+
   | Current cloud as active  | Cassandra->Cassandra                        | GaussDB(for Cassandra) 3.x | Cassandra 2.x                |
   +--------------------------+---------------------------------------------+----------------------------+------------------------------+

Network Preparations
--------------------

DRS supports disaster recovery through a Virtual Private Network (VPN), Direct Connect, or public network. :ref:`Table 3 <drs_01_0305__en-us_topic_0000001160149372_en-us_topic_0000001149034513_table81301656181615>` lists the application scenarios of each network type and required preparations.

.. _drs_01_0305__en-us_topic_0000001160149372_en-us_topic_0000001149034513_table81301656181615:

.. table:: **Table 3** Network types

   +-----------------------+-----------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Network Type          | Application Scenario                                                                                      | Preparations                                                                                                                                                                    |
   +=======================+===========================================================================================================+=================================================================================================================================================================================+
   | VPN                   | Disaster recovery from on-premises databases to cloud databases or between cloud databases across regions | Establish a VPN connection between your local data center and the VPC that hosts the destination database. Before disaster recovery, ensure that the VPN network is accessible. |
   +-----------------------+-----------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Direct Connect        | Disaster recovery from on-premises databases to cloud databases or between cloud databases across regions | Use a dedicated network connection to connect your data center to VPCs.                                                                                                         |
   +-----------------------+-----------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Public network        | Disaster recovery from on-premises databases or other cloud databases to destination databases.           | To ensure network connectivity between the source and destination databases, perform the following operations:                                                                  |
   |                       |                                                                                                           |                                                                                                                                                                                 |
   |                       |                                                                                                           | #. Enable public accessibility.                                                                                                                                                 |
   |                       |                                                                                                           |                                                                                                                                                                                 |
   |                       |                                                                                                           |    Enable public accessibility for the source database based on your service requirements.                                                                                      |
   |                       |                                                                                                           |                                                                                                                                                                                 |
   |                       |                                                                                                           | #. Configure security group rules.                                                                                                                                              |
   |                       |                                                                                                           |                                                                                                                                                                                 |
   |                       |                                                                                                           |    -  Add the EIPs of the disaster recovery instance to the whitelist of the source database for inbound traffic.                                                               |
   |                       |                                                                                                           |    -  If destination databases and the DR instance are in the same VPC, they can communicate with each other by default. You do not need to configure a security group.         |
   |                       |                                                                                                           |                                                                                                                                                                                 |
   |                       |                                                                                                           |    .. note::                                                                                                                                                                    |
   |                       |                                                                                                           |                                                                                                                                                                                 |
   |                       |                                                                                                           |       -  The IP address on the **Configure Source and Destination Databases** page is the EIP of the DR instance.                                                               |
   |                       |                                                                                                           |       -  If SSL is not enabled, backing up confidential data for disaster recovery is not recommended.                                                                          |
   +-----------------------+-----------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 4** Supported network types

   +--------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | DR Direction             | Data Flow                                   | VPC           | Public Network | VPN or Direct Connect |
   +==========================+=============================================+===============+================+=======================+
   | Current cloud as standby | MySQL->MySQL                                | Not supported | Supported      | Supported             |
   +--------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | Current cloud as active  | MySQL->MySQL                                | Not supported | Supported      | Supported             |
   +--------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | Current cloud as standby | MySQL -> GaussDB(for MySQL) primary/standby | Not supported | Supported      | Supported             |
   +--------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | Current cloud as standby | Cassandra->Cassandra                        | Not supported | Supported      | Supported             |
   +--------------------------+---------------------------------------------+---------------+----------------+-----------------------+
   | Current cloud as active  | Cassandra->Cassandra                        | Not supported | Supported      | Supported             |
   +--------------------------+---------------------------------------------+---------------+----------------+-----------------------+
