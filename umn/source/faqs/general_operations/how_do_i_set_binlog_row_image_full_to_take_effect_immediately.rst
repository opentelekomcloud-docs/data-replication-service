:original_name: drs_16_0010.html

.. _drs_16_0010:

How Do I Set binlog_row_image=FULL to Take Effect Immediately?
==============================================================

When migrating MySQL databases, ensure that the **binlog_row_image** parameter of the source database is set to **FULL**. Otherwise, the migration task will fail. After **binlog_row_image** is set to **FULL** in the source database, the setting takes effect only for new sessions. To close old sessions, restart the source database and reset the task during a non-service period.

Setting binlog_row_image to FULL
--------------------------------

-  If the source is an RDS instance on the cloud, change **binlog_row_image** to **FULL** on the RDS console, and then restart the source database and reset the task.
-  If the source database is an on-premises database, perform the following steps:

   #. Log in to the server where the MySQL source database is located.

   #. Manually change the value of **binlog_row_image** in the **my.cnf** configuration file to **FULL** and save the file.

      .. code-block:: text

         binlog_row_image=full

   #. To close old sessions, restart the source database and reset the task during a non-service period.
