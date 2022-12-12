:original_name: drs_04_0125.html

.. _drs_04_0125:

From Cassandra to Cassandra
===========================

Supported Source and Destination Databases
------------------------------------------

.. table:: **Table 1** Supported databases

   +-----------------------------------+-----------------------------------+
   | Service Database                  | DR Database                       |
   +===================================+===================================+
   | -  On-premises databases          | -  GaussDB(for Cassandra)         |
   | -  ECS databases                  |                                   |
   | -  Databases on other clouds      |                                   |
   | -  GaussDB(for Cassandra)         |                                   |
   +-----------------------------------+-----------------------------------+

Prerequisites
-------------

-  You have logged in to the DRS console.
-  For details about the supported DB types and versions, see :ref:`Real-Time Disaster Recovery <drs_01_0305>`.

Suggestions
-----------

.. caution::

   -  During the DR initialization, do not perform DDL operations on the service database. Otherwise, the task may be abnormal.
   -  During DR initialization, ensure that no data is written to the DR database to ensure data consistency before and after DR.

-  The success of DR depends on environment and manual operations. To ensure a smooth DR, perform a DR trial before you start the DR task to help you detect and resolve problems in advance.

-  It is recommended that you start your DR task during off-peak hours to minimize the impact on your services.

   -  If the bandwidth is not limited, initialization of DR will increase query workload of the source database by 50 MB/s and occupy 2 to 4 vCPUs.
   -  To ensure data consistency, tables without a primary key may be locked for 3s during disaster recovery.
   -  The data in the DR process may be locked by other transactions for a long period of time, resulting in read timeout.
   -  If DRS concurrently reads data from a database, it will use about 6 to 10 sessions. The impact of the connections on services must be considered.
   -  If you read a table, especially a large table, during DR, the exclusive lock on that table may be blocked.

-  Data-Level Comparison

   To obtain accurate comparison results, start data comparison at a specified time point during off-peak hours. If it is needed, select **Start at a specified time** for **Comparison Time**. Due to slight time difference and continuous operations on data, data inconsistency may occur, reducing the reliability and validity of the comparison results.

Precautions
-----------

Before creating a DR task, read the following precautions:

.. table:: **Table 2** Precautions

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                              | Restrictions                                                                                                                                                                                               |
   +===================================+============================================================================================================================================================================================================+
   | Service database                  | The source Cassandra database version must be 2.0 or later.                                                                                                                                                |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DR database                       | No keyspace with the same name as the source database exists.                                                                                                                                              |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Precautions                       | -  Ensure that data written to Cassandra is written to DMQ the same time.                                                                                                                                  |
   |                                   | -  Cassandra does not support disaster recovery of system tables and materialized views.                                                                                                                   |
   |                                   | -  Disaster recovery of DDLs is not supported. You need to manually create the corresponding database table structure in the destination database.                                                         |
   |                                   | -  The DR task must be started within 24 hours after the stream table is enabled and data is written.                                                                                                      |
   |                                   | -  Disaster recovery of Cassandra table-level and row-level TTLs is supported. The names of the columns on which the TTLs are applied must be specified. The column cannot be collection, counter, or key. |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Procedure
---------

#. On the **Disaster Recovery Management** page, click **Create Disaster Recovery Task**.
#. On the **Create Disaster Recovery Instance** page, specify the task name, description, and the DR instance details, and click **Next**.

   -  Task information description

      .. table:: **Table 3** Task and recipient description

         +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter   | Description                                                                                                                                      |
         +=============+==================================================================================================================================================+
         | Region      | The region where your service is running. You can change the region.                                                                             |
         +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
         | Project     | The project corresponds to the current region and can be changed.                                                                                |
         +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
         | Task Name   | The task name must start with a letter and consist of 4 to 50 characters. It can contain only letters, digits, hyphens (-), and underscores (_). |
         +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
         | Description | The description consists of a maximum of 256 characters and cannot contain special characters ``!=<>'&"\``                                       |
         +-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

   -  DR instance information

      .. table:: **Table 4** DR instance settings

         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                                                                                                                                                                                                                                  |
         +===================================+==============================================================================================================================================================================================================================================================================================================================+
         | Disaster Recovery Relationship    | Select **Current cloud as standby**.                                                                                                                                                                                                                                                                                         |
         |                                   |                                                                                                                                                                                                                                                                                                                              |
         |                                   | By default, **Current cloud as standby** is selected. You can also select **Current cloud as active**.                                                                                                                                                                                                                       |
         |                                   |                                                                                                                                                                                                                                                                                                                              |
         |                                   | -  **Current cloud as standby**: The DR database is on the current cloud.                                                                                                                                                                                                                                                    |
         |                                   | -  **Current cloud as active**: The service database is on the current cloud.                                                                                                                                                                                                                                                |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Service DB Engine                 | Select **Cassandra**.                                                                                                                                                                                                                                                                                                        |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | DR DB Engine                      | Select **Cassandra**.                                                                                                                                                                                                                                                                                                        |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Network Type                      | The public network is used as an example.                                                                                                                                                                                                                                                                                    |
         |                                   |                                                                                                                                                                                                                                                                                                                              |
         |                                   | Available options: **VPN or Direct Connect** and **Public network**. By default, the value is **Public network**.                                                                                                                                                                                                            |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | DR DB Instance                    | The Cassandra instance you created.                                                                                                                                                                                                                                                                                          |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Disaster Recovery Instance Subnet | Select the subnet where the disaster recovery instance is located. You can also click **View Subnet** to go to the network console to view the subnet where the instance resides.                                                                                                                                            |
         |                                   |                                                                                                                                                                                                                                                                                                                              |
         |                                   | By default, the DRS instance and the destination DB instance are in the same subnet. You need to select the subnet where the DRS instance resides, and there are available IP addresses for the subnet. To ensure that the disaster recovery instance is successfully created, only subnets with DHCP enabled are displayed. |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Migrate TTL                       | If this function is enabled, the TTL of the source Cassandra database is migrated to the destination database. If this function is not enabled, data inconsistency may occur.                                                                                                                                                |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      If a task fails to be created, DRS retains the task for three days by default. After three days, the task automatically ends.

#. On the **Configure Source and Destination Databases** page, wait until the DR instance is created. Then, specify information about the service database, DMQ, and destination database and click **Test Connection** for both the source and destination databases to check whether they have been connected to the DR instance. After the connection tests are successful, select the check box before the agreement and click **Next**.

   .. table:: **Table 5** Service database settings

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                                           |
      +===================================+=======================================================================================================================================================================================================================================================================================================================================================================================+
      | Source Database Type              | Select a service database type.                                                                                                                                                                                                                                                                                                                                                       |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | IP Address or Domain Name         | IP address or domain name of the Cassandra database.                                                                                                                                                                                                                                                                                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Database Username                 | The username for accessing the service database.                                                                                                                                                                                                                                                                                                                                      |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Database Password                 | The password for the service database username. You can change the password if necessary. To change the password, perform the following operation after the task is created:                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                       |
      |                                   | If the task is in the **Starting**, **Initializing**, **Disaster recovery in progress**, or **Disaster recovery failed** status, in the **DR Information** area on the **Basic Information** tab, click **Update Password** next to the **Source Database Password** field. In the displayed dialog box, change the password. This action only updates DRS with the changed password. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      The IP address, domain name, username, and password of the service database are encrypted and stored in DRS and will be cleared after the task is deleted.

   .. table:: **Table 6** DR database settings

      +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                 | Description                                                                                                                                                   |
      +===========================+===============================================================================================================================================================+
      | IP Address or Domain Name | IP address or domain name of the DMQ service.                                                                                                                 |
      +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Database Username         | Username of the DMQ service.                                                                                                                                  |
      +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Database Password         | Password of the DMQ service.                                                                                                                                  |
      +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Group ID                  | Message consumer group of the DMQ service. The system determines how to distribute messages and record the location of the group based on the consumer group. |
      +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Queue Name                | Message type of the DMQ service.                                                                                                                              |
      +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      You can choose whether to enable DMQ information. When the DMQ information is disabled, only inventory data is migrated and incremental data is not synchronized.

   .. table:: **Table 7** DR database settings

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                       |
      +===================================+===================================================================================================================================================================================================================================================================================================================+
      | DB Instance Name                  | The Cassandra instance you selected when you created the DR task. This parameter cannot be changed.                                                                                                                                                                                                               |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Database Username                 | The username for accessing the DR database.                                                                                                                                                                                                                                                                       |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Database Password                 | The password for the DR database username. You can change the password if necessary. To change the password, perform the following operation after the task is created:                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                                                                                   |
      |                                   | If the task is in the starting, initializing, disaster recovery in progress, or disaster recovery failed state, in the **DR Information** area on the **Basic Information** tab, click **Update Password** next to the **Destination Database Password** field. In the displayed dialog box, change the password. |
      |                                   |                                                                                                                                                                                                                                                                                                                   |
      |                                   | The database username and password are encrypted and stored in the system, and will be cleared after the task is deleted.                                                                                                                                                                                         |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the displayed page, configure the required parameters and click **Next**.

   .. table:: **Table 8** DR settings

      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                             | Description                                                                                                                                                                                                 |
      +=======================================+=============================================================================================================================================================================================================+
      | Active Data Center Name               | Name of the active DC. This parameter is left blank by default.                                                                                                                                             |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Concurrent Full Export Threads        | Number of export threads. Value range: 1 to 8. A larger value indicates higher load on the source database.                                                                                                 |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Concurrent Full Import Threads        | Number of import threads. Value range: 1 to 16. A larger value indicates higher load on the destination database.                                                                                           |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Concurrent Incremental Import Threads | Number of concurrent threads for data replay. Value range: 1 to 16. Incremental data is concurrently written to the destination database. A larger value indicates higher load on the destination database. |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Disaster Recovery Object              | Select objects that require disaster recovery based on your service requirements.                                                                                                                           |
      +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Check Task** page, check the DR task.

   -  If any check fails, review the failure cause and rectify the fault. After the fault is rectified, click **Check Again**.

   -  If the check is complete and the check success rate is 100%, click **Next**.

      .. note::

         You can proceed to the next step only when all checks are successful. If there are any items that require confirmation, view and confirm the details first before proceeding to the next step.
