:original_name: drs_11_0064.html

.. _drs_11_0064:

Checking Whether the binlog_row_image Value is FULL
===================================================

MySQL
-----

.. table:: **Table 1** Checking whether the binlog_row_image value is FULL

   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the **binlog_row_image** value is **FULL**                                                                                                              |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | If the **binlog_row_image** value of the source database is not **FULL**, the migration will fail.                                                              |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The **binlog_row_image** value of the source database is not **FULL**.                                                                           |
   |                                       |                                                                                                                                                                 |
   |                                       | Handling suggestion:                                                                                                                                            |
   |                                       |                                                                                                                                                                 |
   |                                       | -  If the source database is an RDS DB instance on the cloud, change **binlog_row_image** to **FULL** on the RDS console, and then restart the source database. |
   |                                       | -  If the source database is an on-premises database, perform the following steps:                                                                              |
   |                                       |                                                                                                                                                                 |
   |                                       |    #. Log in to the server where the MySQL source database is located.                                                                                          |
   |                                       |                                                                                                                                                                 |
   |                                       |    #. Manually change the value of **binlog_row_image** in the **my.cnf** configuration file to **FULL** and save the file.                                     |
   |                                       |                                                                                                                                                                 |
   |                                       |       .. code:: text                                                                                                                                            |
   |                                       |                                                                                                                                                                 |
   |                                       |          binlog_row_image=full                                                                                                                                  |
   |                                       |                                                                                                                                                                 |
   |                                       |    #. To ensure a successful task, restart the source database during off-peak hours.                                                                           |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
