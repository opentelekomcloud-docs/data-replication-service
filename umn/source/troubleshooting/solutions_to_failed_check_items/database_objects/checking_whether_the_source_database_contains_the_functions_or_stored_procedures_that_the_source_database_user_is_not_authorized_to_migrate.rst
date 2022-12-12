:original_name: drs_11_0080.html

.. _drs_11_0080:

Checking Whether the Source Database Contains the Functions or Stored Procedures that the Source Database User Is Not Authorized to Migrate
===========================================================================================================================================

MySQL
-----

.. table:: **Table 1** Checking whether the source database contains the functions or stored procedures that the source database user is not authorized to migrate

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database contains the functions or stored procedures that the source database user is not authorized to migrate. |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | The source database contains the functions or stored procedures that the source database user is not authorized to migrate.         |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The source database user does not have the permission to migrate functions and stored procedures.                    |
   |                                       |                                                                                                                                     |
   |                                       | Handling suggestion: Ensure that the source database user has the highest-level right.                                              |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
