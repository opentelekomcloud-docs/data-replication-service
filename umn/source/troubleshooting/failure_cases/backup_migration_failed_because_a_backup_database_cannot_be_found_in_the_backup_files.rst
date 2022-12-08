:original_name: drs_13_0005.html

.. _drs_13_0005:

Backup Migration Failed Because a Backup Database Cannot Be Found in the Backup Files
=====================================================================================

Scenarios
---------

When you migrate full backups from self-built OBS buckets to clouds, the system displays an error message indicating that the migration failed because the source database cannot be found in the backup files.

Possible Cause
--------------

The name of a .bak backup file uploaded to a self-built OBS bucket is too long.

Solution
--------

Based on the previous analysis, a solution is provided as follows:

#. Change the name of the backup file in the local database and upload the file to a self-built OBS bucket again.
