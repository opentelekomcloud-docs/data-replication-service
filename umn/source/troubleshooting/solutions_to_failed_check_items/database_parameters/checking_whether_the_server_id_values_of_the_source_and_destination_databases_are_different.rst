:original_name: drs_11_0044.html

.. _drs_11_0044:

Checking Whether the SERVER_ID Values of the Source and Destination Databases Are Different
===========================================================================================

MySQL
-----

.. table:: **Table 1** Checking whether the SERVER_ID values of the source and destination databases are different

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the **SERVER_ID** values of the source and destination databases are different                                                   |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the **SERVER_ID** values of the source and destination databases are different. If they are the same, the migration fails. |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The **SERVER_ID** values of the source and destination databases must be different.                                       |
   |                                       |                                                                                                                                          |
   |                                       | Handling suggestion: Change **SERVER_ID** of the source and destination databases to different values.                                   |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
