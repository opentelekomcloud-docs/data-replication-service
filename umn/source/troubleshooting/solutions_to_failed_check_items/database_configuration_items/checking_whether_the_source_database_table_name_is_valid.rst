:original_name: drs_11_0105.html

.. _drs_11_0105:

Checking Whether the Source Database Table Name Is Valid
========================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the source database table name is valid

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database table name is valid                                                                                                                  |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | If the source database table name contains invalid character, the synchronization task fails.                                                                    |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The source database table names contain unsupported characters, non-ASCII characters, or the following characters: ></\\                          |
   |                                       |                                                                                                                                                                  |
   |                                       | Handling suggestion: To solve this problem, perform the following steps:                                                                                         |
   |                                       |                                                                                                                                                                  |
   |                                       | Click **Previous** to return to the **Select Migration Type** page. Select a customized object and do not select the table that contains unsupported characters. |
   |                                       |                                                                                                                                                                  |
   |                                       | Method 2: Change the table name.                                                                                                                                 |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
