:original_name: drs_13_0002.html

.. _drs_13_0002:

Backup Migration Failed Because Backup Files Cannot Be Found
============================================================

Scenarios
---------

When you migrate full backups from self-built OBS buckets to clouds, the following error message is displayed: restore:null.

Possible Causes
---------------

The possible causes are as follows:

-  Backup files are deleted after you submit a backup migration task.
-  When you upload backup files to a self-built OBS bucket, you select **Archive** for **Storage Class**. OBS archive storage offers cloud storage for rarely accessed data. An archive file uploaded for the first time is in the **Not restored** status. As a result, a Microsoft SQL Server DB instance cannot download the file.

Solutions
---------

Based on the previous analysis, solutions are provided as follows:

Solution 1
----------

If the migration fails because you delete the backup files, you can upload the deleted backup files again to a self-built OBS bucket and select **Standard** for **Storage Class**. For details, see **Uploading a File** in *Object Storage Service Console Operation Guide.*

Solution 2
----------

-  If the migration failed because the storage class of your backup files is **Archive**, perform the following steps. If the size of backup files is small, upload the backup files again to an OBS bucket and select **Standard** for **Storage Class**.
-  If the backup files are large in size, log in to the OBS console and click the bucket to which the backup files are uploaded. On the displayed page, choose **Objects** in the navigation pane on the left. On the **Objects** page, select the object to be restored and click **Restore** above the file list. After the status of the backup files becomes **Restored**, submit an offline migration task again.
