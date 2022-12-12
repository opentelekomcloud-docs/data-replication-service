:original_name: drs_11_0066.html

.. _drs_11_0066:

Checking Whether the MongoDB Instance Type Matches the Migration Mode
=====================================================================

MongoDB Migration
-----------------

.. table:: **Table 1** Checking whether the MongoDB instance type matches the migration mode

   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the MongoDB instance type matches the migration mode                                                                            |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the MongoDB instance type matches the migration mode. If not, the migration fails.                                        |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: When a DRS task is created, the source DB instance type is set to **Cluster**, but the source database is not a cluster. |
   |                                       |                                                                                                                                         |
   |                                       | Handling suggestion: If the source DB instance type is set to **Cluster**, ensure that the source database is a cluster database.       |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
