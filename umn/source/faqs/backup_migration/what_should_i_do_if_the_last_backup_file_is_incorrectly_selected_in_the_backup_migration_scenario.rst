:original_name: drs_04_0041.html

.. _drs_04_0041:

What Should I Do If the Last Backup File Is Incorrectly Selected in the Backup Migration Scenario?
==================================================================================================

During the backup migration, If **Last Backup File** is selected by mistake, perform either of the following operations:

-  If you select **Yes** by mistake, the database receives a signal that the restore is complete, and then sets the database to available, making incremental backup migration impossible. In this case, you can only delete the backup database and perform full and incremental backup restoration again.
-  SQL Server does not have the last backup file in a strict sense. If you select **No** by mistake, you can perform an incremental backup (even if no data is changed). During the incremental backup, select **Yes** to complete the migration. The related database becomes available.
