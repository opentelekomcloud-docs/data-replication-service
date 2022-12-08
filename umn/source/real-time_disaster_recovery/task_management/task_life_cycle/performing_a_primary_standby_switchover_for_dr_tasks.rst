:original_name: drs_03_1116.html

.. _drs_03_1116:

Performing a Primary/Standby Switchover for DR Tasks
====================================================

DRS supports primary/standby switchover for DR tasks. If both RPO and RTO are 0, data has been completely migrated to the DR database. Then, you can determine whether to perform a switchover.

-  RPO measures the difference between the data in the service database and the data in the DRS instance. When RPO is 0, all the data in the service database has been migrated to the DRS instance.
-  RTO measures the amount of data being transmitted. When RTO is 0, all transactions on the DRS instance have been completed on the DR database.

Prerequisites
-------------

-  You have logged in to the DRS console.
-  You have created a DR task.

Primary/Standby Switchover
--------------------------

#. On the **Disaster Recovery Management** page, click the target DR task in the **Task Name/ID** column.
#. On the **Basic Information** tab, click the **Disaster Recovery Monitoring** tab.

3. A primary/secondary switchover can be performed only when the task status is disaster recovery in progress. Click **Promote Current Cloud** to promote the current instance to the service database. Click **Demote Current Cloud** to demote the current instance to the disaster recovery database.

   During a primary/secondary switchover, ensure that there is no data written to the database that will be the standby node, and no data will be written to the standby node in the future. The data of the standby node is synchronized only from the primary node. Any other write operations will pollute the data in the standby database, data conflicts occur in the DR center and cannot be resolved.
