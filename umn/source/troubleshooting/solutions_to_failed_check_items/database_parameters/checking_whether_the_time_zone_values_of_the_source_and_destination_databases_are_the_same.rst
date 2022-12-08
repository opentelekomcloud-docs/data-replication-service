:original_name: drs_11_0023.html

.. _drs_11_0023:

Checking Whether the TIME_ZONE Values of the Source and Destination Databases Are the Same
==========================================================================================

MySQL
-----

.. table:: **Table 1** Checking whether the TIME_ZONE values of the source and destination databases are the same

   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the **TIME_ZONE** values of the source and destination databases are the same                                                                                                                                                 |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | The migration fails because the **TIME_ZONE** values of the source and destination databases are different.                                                                                                                           |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The **TIME_ZONE** or **SYSTEM_TIME_ZONE** values of the source and destination databases must be the same.                                                                                                             |
   |                                       |                                                                                                                                                                                                                                       |
   |                                       | Handling suggestion: Change the **TIME_ZONE** value of the destination database to the same as that of the source database, or change the **TIME_ZONE** value of the source database to the same as that of the destination database. |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
