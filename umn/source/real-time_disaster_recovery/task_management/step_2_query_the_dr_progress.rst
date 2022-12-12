:original_name: drs_02_0028.html

.. _drs_02_0028:

Step 2: Query the DR Progress
=============================

After a DR task starts, you can check the DR progress.

Prerequisites
-------------

-  You have logged in to the DRS console.
-  A DR task has been created and started.

Procedure
---------

#. On the **Disaster Recovery Management** page, click the target DR task in the **Task Name/ID** column.
#. On the displayed page, click the **Disaster Recovery Progress** tab to view the DR progress. When the data initialization is complete, the initialization progress is displayed as 100%.

   -  On the **Disaster Recovery Progress** tab, you can view the DR synchronization delay,
   -  You can also view the DR synchronization delay on the **Disaster Recovery Management** page. When the synchronization delay exceeds the preset or default threshold, the value of the synchronization delay is displayed in red in the task list.
   -  When the delay is 0, data is synchronized from the service database to the DR database in real-time.

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
