:original_name: drs_03_0024.html

.. _drs_03_0024:

Viewing DR Metrics
==================

DRS monitors the DB instance performance and the migration progress. With the monitoring information, you can determine the data flow health status, data integrity, and data consistency. If both RPO and RTO are 0, data has been completely migrated to the DR database. Then, you can determine whether to perform a switchover. Monitoring information cannot be viewed for DR tasks from Cassandra to GaussDB(for Cassandra).

Prerequisites
-------------

-  You have logged in to the DRS console.
-  You have created a DR task.

Procedure
---------

#. On the **Disaster Recovery Management** page, click the target DR task in the **Task Name/ID** column.
#. On the **Basic Information** tab, click the **Disaster Recovery Monitoring** tab.

   -  Recovery Point Objective (RPO) measures the consistency between the data in the service database and the data in the DRS instance. When RPO is 0, all the data in the service database has been migrated to the DRS instance.
   -  Recovery Time Objective (RTO) measures the amount of data being transmitted. When RTO is 0, all transactions on the DRS instance have been completed on the DR database.
   -  Delay: Monitors the historical RPO and RTO, which helps predict the amount of lost data if a disaster occurs. You can pay attention to the following time ranges during which:

      -  The RPO or RTO is high for a long time.
      -  The RPO or RTO is consistently high or spiking high on a regular basis.

   -  Autonomy Management: Monitors the following DRS intelligent autonomy capabilities:

      -  Number of times that DRS automatically resumes data transfer after a network is disconnected
      -  Number of times that DRS automatically overwrites old data with the latest data when a data conflict occurs

   -  Performance: You can use performance monitoring to help diagnose the network quality.
   -  Resource: You can use resource monitoring to help determine whether to scale up the DRS instance specifications.
