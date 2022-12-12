:original_name: drs_01_0005.html

.. _drs_01_0005:

Basic Concepts
==============

VPC
---

VPC-based migration refers to a real-time migration that the source and destination databases are in the same VPC or two VPCs that can communicate with each other. No additional network services are required.

VPN
---

VPN-based migration refers to a real-time migration where the source and destination databases are in the same VPN network. The VPN establishes a secure, encrypted communication tunnel that complies with industry standards between your data centers and the cloud platform. Through this tunnel, DRS seamlessly migrates data from the data center to the cloud.

Direct Connect
--------------

Direct Connect enables you to establish a dedicated network connection from your data center to the cloud platform. With Direct Connect, you can use a dedicated network connection to connect your data center to VPCs to enjoy a high-performance, low-latency, and secure network.

Replication Instance
--------------------

A replication instance refers to an instance that performs the migration task. It exists in the whole lifecycle of a migration task. DRS uses the replication instance to connect to the source database, read source data, and replicate the data to the destination database.

Migration Log
-------------

A migration log refers to the log generated during database migration. Migration logs are classified into the following levels: warning, error, and info.

Task Check
----------

Before starting a migration task, you need to check whether the source and destination databases have met all migration requirements. If any check item fails, rectify the fault and check the task again. Only when all check items are successful the task can start.

To the Cloud
------------

DRS requires that either the source or destination database is on the current cloud. **To the cloud** means that the destination database must be on the current cloud.

Out of the Cloud
----------------

DRS requires that either the source or destination database is on the current cloud. **Out of the cloud** means that the source database must be on the current cloud.

Current Cloud as Standby
------------------------

If you select **Current cloud as standby** for **Disaster Recovery Relationship**, it means that the DR database is a database on the current cloud.

Current Cloud as Active
-----------------------

If you select **Current cloud as active** for **Disaster Recovery Relationship**, it means that the service database is a database on the current cloud.

Region and AZ
-------------

A region and availability zone (AZ) identify the location of a data center. You can create resources in a specific region and AZ.

-  A region is a physical data center. Each region is completely independent, improving fault tolerance and stability. After a resource is created, its region cannot be changed.
-  An AZ is a physical location using independent power supplies and networks. Faults in an AZ do not affect other AZs. A region can contain multiple AZs, which are physically isolated but interconnected through internal networks. This ensures the independence of AZs and provides low-cost and low-latency network connections.

:ref:`Figure 1 <drs_01_0005__en-us_topic_0000001205747781_en-us_topic_0000001102434640_en-us_topic_0171122769_fig2922183194716>` shows the relationship between regions and AZs.

.. _drs_01_0005__en-us_topic_0000001205747781_en-us_topic_0000001102434640_en-us_topic_0171122769_fig2922183194716:

.. figure:: /_static/images/en-us_image_0000001341254148.png
   :alt: **Figure 1** Region and AZ

   **Figure 1** Region and AZ

Project
-------

A project corresponds to a region. Projects group and isolate resources (including compute, storage, and network resources) across physical regions. Users can be granted permissions in a default project to access all resources in the region associated with the project. If you need more refined access control, create subprojects under a default project and create resources in subprojects. Then you can assign users the permissions required to access only the resources in the specific subprojects.


.. figure:: /_static/images/en-us_image_0000001341094488.gif
   :alt: **Figure 2** Project isolating model

   **Figure 2** Project isolating model

Account Entrustment
-------------------

DRS will entrust your account to the administrator to implement some functions. For example, if you enable scheduled startup tasks, DRS will automatically entrust your account to DRS administrator **op_svc_rds** during the task creation to implement automated management on the scheduled tasks.

Account entrustment can be implemented in the same region only.

Temporary Accounts
------------------

To ensure that your database can be successfully migrated to RDS MySQL DB instances, DRS automatically creates temporary accounts **drsFull** and **drsIncremental** in the destination database during full migration and incremental migration, respectively. After the migration task is complete, DRS automatically deletes the temporary account.

.. important::

   Attempting to delete, rename, or change the passwords or permissions for these accounts will cause task errors.

High Availability
-----------------

If the primary host of a replication instance fails, it automatically fails over to the standby host, preventing service interruption and improving the success rate of migration.

If a replication instance fails, the system will automatically restart the instance and retry the task. In this case, the task status changes to **Fault rectification**. If the replication instance is still faulty after being restarted, the system automatically creates an instance. After the instance is created, the system retries the task again. The high availability management applies to the following tasks:

-  Full migration
-  Incremental migration
