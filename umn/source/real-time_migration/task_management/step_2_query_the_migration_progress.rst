:original_name: drs_02_0006.html

.. _drs_02_0006:

Step 2: Query the Migration Progress
====================================

The migration progress of a real-time migration task helps you keep track of the status of the migration task.

DRS shows the migration progress using a progress bar, helping you learn the migration progress in real time. During full migration, you can check migration details.

-  With the progress bar, you can view the migration progress of structures, data, and indexes. When the progress reaches 100%, the migration is complete. The migration of data and indexes is relatively slow.
-  In the migration details, you can view the migration progress of a specific object. If the number of objects is the same as that of migrated objects, the migration is complete. You can view the migration progress of each object in detail. During incremental migration, the progress details are not displayed. You can view the consistency status on the **Migration Comparison** tab.

Prerequisites
-------------

-  You have logged in to the DRS console.
-  A migration task has been started.

Procedure
---------

#. On the **Online Migration Management** page, click the target migration task name in the **Task Name/ID** column.
#. On the displayed page, click **Migration Progress**.

   -  View the migration progress of structures, data, and indexes.

      When a full migration is complete, the progress of each item reaches 100%.

      For a full plus incremental migration, you can view the delay of the incremental migration on the **Migration Progress** page.

      You can also view the incremental migration delay on the **Online Migration Management** page. When the incremental migration delay exceeds the preset or default threshold, the value of the incremental migration delay is displayed in red in the task list.

      .. note::

         "Delay" refers to the delay from when the transaction was submitted to the source database to when it is synchronized to the destination database and executed.

         Transactions are synchronized as follows:

         a. Data is extracted from the source database.
         b. The data is transmitted over the network.
         c. DRS parses the source logs.
         d. The transaction is executed on the destination database.

         If the delay is 0, the source database is consistent with the destination database, and no new transactions need to be synchronized.

      .. caution::

         Frequent DDL operations, ultra-large transactions, and network problems may result in excessive synchronization delay.

   -  View the migration task progress. In the **Migration Details** area, locate the target migration object and click **View Details** in the **Operation** column to view the migration progress. After the incremental migration starts, the progress is not displayed. You can click the **Migration Comparison** tab to compare the data consistency.
