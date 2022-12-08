:original_name: drs_10_0007.html

.. _drs_10_0007:

Step 2: Query the Synchronization Progress
==========================================

This section describes how to check the synchronization progress.

-  During a full synchronization, DRS displays the progress overview. You can view the structure, data, and index migration progress. When the progress reaches 100%, the synchronization is complete. The synchronization of data and indexes is relatively slow.
-  During an incremental synchronization, DRS displays the incremental synchronization delay. You can determine the synchronization status between the source and destination databases based on the delay. If the delay is 0, the source and destination databases are instantaneously consistent, and no new transaction needs to be synchronized.

Prerequisites
-------------

You have logged in to the DRS console.

Procedure
---------

#. On the **Data Synchronization Management** page, click the target synchronization task name in the **Task Name/ID** column.
#. On the displayed page, click **Synchronization Progress** to view table synchronization progress.

   -  When a full synchronization is complete, the progress reaches 100%.
   -  After the full synchronization is complete, the incremental synchronization starts. You can view the incremental synchronization delay on the **Synchronization Progress** tab.
   -  You can also view the incremental synchronization delay on the **Data Synchronization Management** page. When the incremental synchronization delay exceeds the preset or default threshold, the value of the incremental synchronization delay is displayed in red in the task list.
   -  When the delay is 0s, the data in the source and destination databases is synchronized in real time.

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
