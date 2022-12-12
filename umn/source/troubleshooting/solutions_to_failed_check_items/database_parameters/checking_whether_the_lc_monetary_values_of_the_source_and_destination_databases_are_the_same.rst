:original_name: drs_11_0038.html

.. _drs_11_0038:

Checking Whether the lc_monetary Values of the Source and Destination Databases Are the Same
============================================================================================

PostgreSQL Synchronization
--------------------------

.. table:: **Table 1** Checking whether the lc_monetary values of the source and destination databases are the same

   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the **lc_monetary** values of the source and destination databases are the same                                                             |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the **lc_monetary** values of the source and destination databases are the same. If they are inconsistent, the synchronization fails. |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: This item cannot be checked because the source database failed to be connected.                                                      |
   |                                       |                                                                                                                                                     |
   |                                       | Handling suggestion: Check whether the source database is connected.                                                                                |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: This item cannot be checked because the destination database failed to be connected.                                                 |
   |                                       |                                                                                                                                                     |
   |                                       | Handling suggestion: Check whether the destination database is connected.                                                                           |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The **lc_monetary** values of the source and destination databases must be the same.                                                 |
   |                                       |                                                                                                                                                     |
   |                                       | Handling suggestion: Check whether the **lc_monetary** values of the source and destination databases meet the synchronization requirements.        |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Insufficient user permissions                                                                                                        |
   |                                       |                                                                                                                                                     |
   |                                       | Handling suggestion: Check whether the database user permissions meet the synchronization requirements.                                             |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                                            |
   |                                       |                                                                                                                                                     |
   |                                       | Handling suggestion: Contact technical support.                                                                                                     |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
