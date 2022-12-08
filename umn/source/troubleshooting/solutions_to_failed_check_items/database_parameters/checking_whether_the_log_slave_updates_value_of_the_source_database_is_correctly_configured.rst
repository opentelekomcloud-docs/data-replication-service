:original_name: drs_11_0061.html

.. _drs_11_0061:

Checking Whether the log_slave_updates Value of the Source Database Is Correctly Configured
===========================================================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the log_slave_updates value of the source database is correctly configured

   +----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                                   | Whether the **log_slave_updates** value of the source database is correctly configured                                                                                                                               |
   +----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                                  | The migration will fail if the **log_slave_updates** parameter of the source database is disabled.                                                                                                                   |
   +----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion        | Failure cause: The **slave_updates_check** parameter of the source database must be enabled.                                                                                                                         |
   |                                              |                                                                                                                                                                                                                      |
   |                                              | Handling suggestion: In the MySQL configuration file **my.cnf**, add the "log_slave_updates=1" line under [mysqld] and restart the database for the modification to take effect.                                     |
   +----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                              | Failure cause: The source database is a standby database and the **log_slave_updates** value is **OFF**.                                                                                                             |
   |                                              |                                                                                                                                                                                                                      |
   |                                              | Handling suggestion: On the source database, set **log_slave_updates** to **ON**. Then, restart the database for the modification to take effect.                                                                    |
   +----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item to Be Confirmed and Handling Suggestion | Item to be confirmed: The source database is a standby database and the **log_slave_updates** value is **OFF**.                                                                                                      |
   |                                              |                                                                                                                                                                                                                      |
   |                                              | Handling suggestion: On the source database, set **log_slave_updates** to **ON**. Then, restart the database for the modification to take effect. If no switchover or failover will occur, no operation is required. |
   +----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
