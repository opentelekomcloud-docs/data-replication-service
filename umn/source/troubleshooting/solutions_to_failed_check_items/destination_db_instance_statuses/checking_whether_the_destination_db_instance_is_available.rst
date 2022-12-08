:original_name: drs_11_0230.html

.. _drs_11_0230:

Checking Whether the Destination DB Instance Is Available
=========================================================

.. table:: **Table 1** Checking whether the destination DB instance is available

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination DB instance is available                                                                             |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the primary instance and read replicas are available in the destination database. If not, the migration fails. |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The destination DB instance is not available.                                                                 |
   |                                       |                                                                                                                              |
   |                                       | Handling suggestion: Repair the destination DB instance.                                                                     |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Read replicas in the destination database are abnormal.                                                       |
   |                                       |                                                                                                                              |
   |                                       | Handling suggestion: Repair the abnormal read replicas in the destination database.                                          |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The RDS service is abnormal. Try again later.                                                                 |
   |                                       |                                                                                                                              |
   |                                       | Handling suggestion: Try again later.                                                                                        |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
