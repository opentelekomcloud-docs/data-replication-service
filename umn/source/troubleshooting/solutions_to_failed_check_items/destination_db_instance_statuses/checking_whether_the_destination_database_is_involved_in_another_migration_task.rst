:original_name: drs_11_0011.html

.. _drs_11_0011:

Checking Whether the Destination Database Is Involved in Another Migration Task
===============================================================================

MySQL
-----

.. table:: **Table 1** Checking whether the destination database is involved in another migration task

   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination database is involved in another migration task                                                                                                      |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the destination database is being used in another migration task. If more than one migration task uses the same destination database, the migration may fail. |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The destination RDS DB instance is being used in another migration task.                                                                                     |
   |                                       |                                                                                                                                                                             |
   |                                       | Handling suggestion: Wait for the migration task to complete. You can also stop or delete an unused migration task.                                                         |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
