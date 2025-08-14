:original_name: drs_11_0226.html

.. _drs_11_0226:

Checking Whether GTID Is Enabled for the Source Database
========================================================

MySQL
-----

.. table:: **Table 1** Checking whether GTID is enabled for the source database

   +----------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                                   | Whether GTID is enabled for the source database                                                                                                                              |
   +----------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                                  | During disaster recovery, GTID should be enabled for the source database. Otherwise, the migration fails.                                                                    |
   +----------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item to Be Confirmed and Handling Suggestion | Failure cause: GTID is disabled for the source database                                                                                                                      |
   |                                              |                                                                                                                                                                              |
   |                                              | Handling suggestion: In the configuration file of the source database, set parameters as followings. Then, restart the source database for the modifications to take effect. |
   |                                              |                                                                                                                                                                              |
   |                                              | Parameters to be configured:                                                                                                                                                 |
   |                                              |                                                                                                                                                                              |
   |                                              | .. code:: text                                                                                                                                                               |
   |                                              |                                                                                                                                                                              |
   |                                              |    gtid_mode = on;                                                                                                                                                           |
   |                                              |    log_slave_updates = true;                                                                                                                                                 |
   |                                              |    enforce_gtid_consistency = on;                                                                                                                                            |
   +----------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
