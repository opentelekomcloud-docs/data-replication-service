:original_name: drs_11_0004.html

.. _drs_11_0004:

Checking Whether the Names of the Source and Destination Databases Are the Same
===============================================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the names of the source and destination databases are the same

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the names of the source and destination databases are the same                                                                                                                                |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the names of the source and destination databases are the same.                                                                                                                         |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: This item cannot be checked because the source database fails to be connected.                                                                                                         |
   |                                       |                                                                                                                                                                                                       |
   |                                       | Handling suggestion: Check whether the source database is connected.                                                                                                                                  |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: This item cannot be checked because the destination database fails to be connected.                                                                                                    |
   |                                       |                                                                                                                                                                                                       |
   |                                       | Handling suggestion: Check whether the destination database is connected.                                                                                                                             |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Insufficient user permissions                                                                                                                                                          |
   |                                       |                                                                                                                                                                                                       |
   |                                       | Handling suggestion: Check whether the database user permissions meet the migration requirements.                                                                                                     |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Handling suggestion:                                                                                                                                                                                  |
   |                                       |                                                                                                                                                                                                       |
   |                                       | -  If you are migrating data to the cloud, determine whether to delete the databases with the same names as the source databases or specify a new destination DB instance based on site requirements. |
   |                                       | -  If you are migrating data out of the cloud, determine whether to use the original destination database or specify a new destination DB instance based on site requirements.                        |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: During an incremental migration, the source and destination databases cannot have the same names.                                                                                      |
   |                                       |                                                                                                                                                                                                       |
   |                                       | Handling suggestion: Determine whether to retain these databases in the destination RDS DB instance or specify another destination RDS DB instance.                                                   |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                                                                                              |
   |                                       |                                                                                                                                                                                                       |
   |                                       | Handling suggestion: Contact technical support.                                                                                                                                                       |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
