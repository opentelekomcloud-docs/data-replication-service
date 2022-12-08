:original_name: drs_11_0022.html

.. _drs_11_0022:

Checking Whether the Source Database Contains Object Names with Non-ASCII Characters
====================================================================================

MySQL
-----

.. table:: **Table 1** Checking whether the source database contains object names with non-ASCII characters

   +---------------------------------------+------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database contains object names with non-ASCII characters                          |
   +---------------------------------------+------------------------------------------------------------------------------------------------------+
   | Description                           | If the source database contains object names with non-ASCII characters, the migration will fail.     |
   +---------------------------------------+------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The source database cannot contain object names with non-ASCII characters.            |
   |                                       |                                                                                                      |
   |                                       | Handing suggestion: In the source database, change the object names containing non-ASCII characters. |
   +---------------------------------------+------------------------------------------------------------------------------------------------------+
