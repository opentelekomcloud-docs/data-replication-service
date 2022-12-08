:original_name: drs_11_0045.html

.. _drs_11_0045:

Checking Whether the Source Database Name Is Valid
==================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the source database name is valid

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database name is valid                                                                                                                                                      |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | The source database name cannot contain invalid characters. It must contain 1 to 64 characters, including only lowercase letters, digits, hyphens (-), and underscores (_).                    |
   |                                       |                                                                                                                                                                                                |
   |                                       | If the source database name contains any invalid character, the migration fails.                                                                                                               |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: This item cannot be checked because the source database fails to be connected.                                                                                                  |
   |                                       |                                                                                                                                                                                                |
   |                                       | Handling suggestion: Check whether the source database is connected.                                                                                                                           |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The source database name cannot contain invalid characters. It must contain 1 to 64 characters, including only lowercase letters, digits, hyphens (-), and underscores (_).     |
   |                                       |                                                                                                                                                                                                |
   |                                       | Handling suggestion: Change the source database names that contain unsupported characters or go back to the previous page and select the databases that do not contain unsupported characters. |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
