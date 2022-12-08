:original_name: drs_11_0025.html

.. _drs_11_0025:

Checking Whether the SERVER_UUID Values of the Source and Destination Databases Are the Same
============================================================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the SERVER_UUID values of the source and destination databases are the same

   +---------------------------------------+----------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the **SERVER_UUID** values of the source and destination databases are the same                  |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------+
   | Description                           | If the **SERVER_UUID** values of the source and destination databases are the same, the migration fails. |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The **SERVER_UUID** values of the source and destination databases must be different.     |
   |                                       |                                                                                                          |
   |                                       | Handling suggestion: Check that the source and destination databases are not the same MySQL database.    |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------+
