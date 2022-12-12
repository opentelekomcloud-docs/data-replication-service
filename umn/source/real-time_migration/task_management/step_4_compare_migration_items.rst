:original_name: drs_02_0007.html

.. _drs_02_0007:

Step 4: Compare Migration Items
===============================

This section describes how to compare migration items to check if there are any differences between source and destination databases. By comparing migration objects, you can determine the proper time for service migration to minimize the service downtime.


.. figure:: /_static/images/en-us_image_0000001391773841.png
   :alt: **Figure 1** Comparison process

   **Figure 1** Comparison process

Comparison Scenarios
--------------------

You can compare migration objects with different dimensions:

-  Object-level comparison: It helps you compare databases, indexes, tables, views, stored procedures and functions, and sorting rules of tables. You are advised to perform the comparison after a full migration is complete.
-  Data-level comparison is classified into row comparison and value comparison.

   -  Row comparison: It helps you compare the number of rows in the tables to be migrated. This comparison method is recommended because it is fast.
   -  Value comparison: It helps you check whether data in the migrated table is consistent. The comparison process is relatively slow.

When you check data consistency, compare the number of rows first. If the number of rows are inconsistent, you can then compare the data in the table to determine the inconsistent data.

Comparison Restrictions
-----------------------

-  A comparison task can be created only when the task is in the incremental phase. When a full task is complete, DRS automatically creates object-level and row comparison tasks.
-  If DDL operations were performed on the source database, you need to compare the objects again to ensure the accuracy of the comparison results.
-  If data in the destination database is modified separately, the comparison results may be inconsistent.
-  Currently, only tables with primary keys support value comparison. For tables that do not support value comparison, you can compare rows. Therefore, you can compare data by row or value based on scenarios.
-  To prevent resources from being occupied for a long time, DRS limits the row comparison duration. If the row comparison duration exceeds the threshold, the row comparison task stops automatically. If the source database is a relational database, the row comparison duration is 60 minutes. If the source database is a non-relational database, for example, MongoDB, the row comparison duration is 30 minutes.

Impact on Databases
-------------------

-  Object comparison: System tables of the source and destination databases are queried, occupying about 10 sessions. The database is not affected. However, if there are a large number of objects (for example, hundreds of thousands of tables), the database may be overloaded.
-  Row comparison: The number of rows in the source and destination databases is queried, which occupies about 10 sessions. The SELECT COUNT statement does not affect the database. However, if a table contains a large amount of data (hundreds of millions of records), the database will be overloaded and the query results will be returned slowly.
-  Value comparison: All data in the source and destination databases is queried, and each field is compared. The query pressure on the database leads to high I/O. The query speed is limited by the I/O and network bandwidth of the source and destination databases. Value comparison occupies one or two CPUs, and about 10 sessions.

Estimated Comparison Duration
-----------------------------

-  Object comparison: Generally, the comparison results are returned within several minutes based on the query performance of the source database. If the amount of data is large, the comparison may take dozens of minutes.
-  Row comparison: The SELECT COUNT method is used. The query speed depends on the database performance.
-  Value comparison: If the database workload is not heavy and the network is normal, the comparison speed is about 5 MB/s.

Prerequisites
-------------

-  You have logged in to the DRS console.
-  A migration task has been started.

Creating a comparison task
--------------------------

You can follow the comparison process or select a comparison method based on your service scenario. The following operations describe how to compare migration items by following the recommended migration process.

#. On the **Online Migration Management** page, click the target migration task name in the **Task Name/ID** column.
#. On the **Migration Comparison** tab, compare objects of the source and destination databases.

   a. Check the integrity of the database object.

      Click **Validate Objects**. On the **Object-Level Comparison** tab, view the comparison result of each comparison item.

      Locate a comparison item you want to view and click **View Details** in the **Operation** column.

   b. .. _drs_02_0007__li28278341571:

      After the check is complete, compare the number of rows and values.

      #. In the **Before You Start** pane, click **Validate All Rows/Values**.

      #. In the displayed **Create Comparison Task** dialog box, specify **Comparison Type**, **Comparison Time**, and **Object**. Then, click **OK**.

         -  **Comparison Type**: compares rows and values.
         -  **Comparison Time**: You can select **Start upon task creation** or **Start at a specified time**. There is a slight difference in time between the source and destination databases during synchronization. Data inconsistency may occur. You are advised to compare migration items during off-peak hours for more accurate results.
         -  **Object**: You can select objects to be compared based on the scenarios.

         After the comparison creation task is submitted, the **Data-Level Comparison** tab is displayed. Click |image1| to refresh the list and view the comparison result of the specified comparison type.

         To view the comparison details, locate the target comparison type and click **View Results** in the **Operation** column. On the displayed page, locate a pair of source and destination databases, and click **View Details** in the **Operation** column to view detailed comparison results.

         .. note::

            You can cancel a running task at any time and view the comparison report of a canceled comparison task.

   c. Perform a double check before the cutover.

      Click **Double Check During Cutover**. In the displayed **Create Comparison Task** dialog box, specify **Comparison Type**, **Comparison Time**, and **Object**. Then, click **OK**.

      For details about how to view comparison details, see :ref:`2.b <drs_02_0007__li28278341571>`.

   d. Stop the migration task.

      After the service system is successfully migrated to the destination database, stop the migration task to prevent operations in the source database from being synchronized to the destination database to overwrite the data. This operation only deletes the replication instance, and the migration task is still in the task list. You can view or delete the task.

      Generally, stopping a task can ensure the integrity of special objects because triggers and events are migrated when a task is being stopped. Only in some cases, such as network disconnections, a task may fail to be stopped. If a task fails to be stopped multiple times, you can select **Forcibly stop task** to reduce the waiting time. If you forcibly stop a task, triggers and events may not be completely migrated and you need to manually migrate them.

Quick Comparison
----------------

To accelerate and simplify the migration process, DRS provides the quick comparison function. You can directly perform a comparison on the migration task list. This function can be used to compare all migration objects only when incremental migration tasks are in progress.

#. On the **Online Migration Management** page, locate the target migration task and click **Compare** in the **Operation** column.
#. On the **Create Comparison Task** page, select **Start upon task creation** or **Start at a specified time** and click **Yes** to start the comparison task.

Viewing a Comparison Task
-------------------------

#. On the **Online Migration Management** page, locate the target migration task and click **View** in the **Operation** column.
#. On the **Migration Comparison** tab, view the data comparison result.

.. |image1| image:: /_static/images/en-us_image_0000001391773845.png
