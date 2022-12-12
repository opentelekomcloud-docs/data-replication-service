:original_name: drs_10_0012.html

.. _drs_10_0012:

Step 4: Compare Synchronization Items
=====================================

Scenarios
---------

This section describes how to compare synchronization items to check if there are any differences between source and destination databases. To minimize the impact on services and shorten the service interruption duration, the following comparison methods are provided:

-  Object-level comparison: compares objects such as databases, indexes, tables, views, stored procedures, functions, and table sorting rules.
-  Data-level comparison is classified into row comparison and value comparison.

   -  Row comparison: It helps you compare the number of rows in the tables to be synchronized. This comparison method is recommended because it is fast.
   -  Value comparison: It helps you check whether data in the synchronized table is consistent. The comparison process is relatively slow.

-  Account comparison: It compares usernames and permissions of the source and destination databases.

When you check data consistency, compare the number of rows first. If the number of rows are inconsistent, you can then compare the data in the table to determine the inconsistent data.

Constraints
-----------

-  A comparison task can be created only when the task is in the incremental phase. When a full task is complete, DRS automatically creates object-level and row comparison tasks.
-  If DDL operations were performed on the source database, you need to compare the objects again to ensure the accuracy of the comparison results.
-  If data in the destination database is modified separately, the comparison results may be inconsistent.
-  Currently, only tables with primary keys support value comparison. For tables that do not support value comparison, you can compare rows. Therefore, you can compare data by row or value based on scenarios.
-  To prevent resources from being occupied for a long time, DRS limits the row comparison duration. If the row comparison duration exceeds the threshold, the row comparison task stops automatically. If the source database is a relational database, the row comparison duration is 60 minutes. If the source database is a non-relational database, for example, MongoDB, the row comparison duration is 30 minutes.

-  In the many-to-one row comparison scenario, the number of rows in the table in the source database is compared with that in the aggregation table mapped to the destination database.
-  If the source is a PostgreSQL database, the index and constraint names will be changed during table mapping. As a result, the index and constraint names are inconsistent.

Prerequisites
-------------

-  You have logged in to the DRS console.
-  A synchronization task has been started.

Creating a Comparison Task
--------------------------

#. On the **Data Synchronization Management** page, click the target synchronization task name in the **Task Name/ID** column.

#. Click the **Synchronization Comparison** tab.

#. Compare synchronization items.

   -  On the **Object-Level Comparison** tab, check whether the comparison results of the source and destination databases are consistent. Locate a comparison item you want to view and click **View Details** in the **Operation** column.
   -  On the **Data-Level Comparison** tab, click **Create Comparison Task**. In the displayed dialog box, specify **Comparison Type**, **Comparison Time**, and **Object**. Then, click **OK**.

      -  **Comparison Type**: compares rows and values.

         -  Row comparison: checks whether the source table has the same number of rows as the destination table.

            .. note::

               -  After a task enters the incremental comparison phase, you can create a row comparison task.

         -  Value comparison: checks whether the source table has the same data as the destination table.

            .. note::

               -  After a task enters the incremental synchronization phase, you can create a value comparison task. After the full synchronization is complete, data in the source database cannot be changed. Otherwise, the comparison result will be inconsistent.

            Value comparison only applies to tables with single-column primary key or unique index. You can use row comparison for tables that do not support value comparison. Therefore, you can compare data by row or value based on scenarios.

      -  **Comparison Policy**: DRS supports one-to-one and many-to-one comparison policies.

         -  **One-to-one**: compares the number of rows in a table in the source database with that in the table mapped to the destination database.
         -  **Many-to-one**: compares the number of rows in a table in the source database with that in the aggregate table mapped to the destination database.

            .. note::

               If you select **Row Comparison** for **Comparison Type**, the **Comparison Policy** option becomes available.

      -  **Comparison Time**: You can select **Start upon task creation** or **Start at a specified time**. There is a slight difference in time between the source and destination databases during synchronization. Data inconsistency may occur. You are advised to compare migration items during off-peak hours for more accurate results.
      -  **Object**: You can select objects to be compared based on the scenarios.

   -  User comparison: Click the User Comparison tab to view the comparison results of database accounts and permissions.

      .. note::

         -  Full synchronization tasks do not support account comparisons.
         -  Only PostgreSQL to PostgreSQL synchronization supports account comparison.

#. After the comparison creation task is submitted, the **Data-Level Comparison** tab is displayed. Click |image1| to refresh the list and view the comparison result of the specified comparison type.

   Value comparison only applies to tables with single-column primary key or unique index. You can use row comparison for tables that do not support value comparison. Therefore, you can compare data by row or value based on scenarios.

   If you want to view the row or value comparison details, click **View Results**.

   If you want to download the row comparison or value comparison result, locate a specified comparison type and click **Export Report** in the **Operation** column.

   .. note::

      You can also view comparison details of canceled comparison tasks.

.. |image1| image:: /_static/images/en-us_image_0000001341094428.png
