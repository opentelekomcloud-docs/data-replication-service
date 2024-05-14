:original_name: drs_11_0043.html

.. _drs_11_0043:

Checking Whether the Destination Database Contains a Non-Empty Collection with the Same Name As the Source Database
===================================================================================================================

Migration from MongoDB to DDS
-----------------------------

.. table:: **Table 1** Checking whether the destination database contains a non-empty collection with the same name as the source database

   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination database contains a non-empty collection with the same name as the source database                                                                                                                                         |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the source and destination databases have the same non-empty collections to prevent existing databases from being overwritten. If the source and destination databases have the same collections, the migration cannot be performed. |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: This item cannot be checked because the source database failed to be connected.                                                                                                                                                     |
   |                                       |                                                                                                                                                                                                                                                    |
   |                                       | Handling suggestion: Check whether the source database is connected.                                                                                                                                                                               |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: This item cannot be checked because the destination database failed to be connected.                                                                                                                                                |
   |                                       |                                                                                                                                                                                                                                                    |
   |                                       | Handling suggestion: Check whether the destination database is connected.                                                                                                                                                                          |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The same non-empty collections exist in both the source and destination databases.                                                                                                                                                  |
   |                                       |                                                                                                                                                                                                                                                    |
   |                                       | Handling suggestion: Determine whether to delete the same non-empty collections from the destination DB instance or specify a new destination DB instance.                                                                                         |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                                                                                                                                           |
   |                                       |                                                                                                                                                                                                                                                    |
   |                                       | Handling suggestion: Contact technical support.                                                                                                                                                                                                    |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
