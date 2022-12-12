:original_name: drs_11_0016.html

.. _drs_11_0016:

Checking Whether the Binlog Retention Period Is Set on the Source Database
==========================================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the binlog retention period is set on the source database

   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the binlog retention period is set on the source database                                                                                                                      |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Checking whether the binlog retention period is set on the source database. You are advised to store the source database binlog for a longer time, if the storage space is sufficient. |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The binlog retention period is not set on the source database.                                                                                                          |
   |                                       |                                                                                                                                                                                        |
   |                                       | Handling suggestion:                                                                                                                                                                   |
   |                                       |                                                                                                                                                                                        |
   |                                       | Log in to the source database and run the following SQL statement to set the retention period of binlog:                                                                               |
   |                                       |                                                                                                                                                                                        |
   |                                       | .. code:: text                                                                                                                                                                         |
   |                                       |                                                                                                                                                                                        |
   |                                       |    call mysql.rds_set_configuration('binlog retention hours', n);                                                                                                                      |
   |                                       |                                                                                                                                                                                        |
   |                                       | The value **n** indicates an integer from 1 to 168.                                                                                                                                    |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
