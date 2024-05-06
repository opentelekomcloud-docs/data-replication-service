:original_name: drs_11_0200.html

.. _drs_11_0200:

Checking Whether the Source Database Collections Contain More Than 10 Indexes
=============================================================================

Migration from MongoDB to DDS
-----------------------------

.. table:: **Table 1** Checking whether the source database collections contain more than 10 indexes

   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database collections contain more than 10 indexes                                                                                                                                                 |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | If the number of indexes in the source database exceeds 10, the migration duration is affected.                                                                                                                      |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Alarm cause: The source database has collections containing more than 10 indexes, which are migrated slowly.                                                                                                         |
   |                                       |                                                                                                                                                                                                                      |
   |                                       | Handling suggestion: The number of indexes affects the migration duration. Check whether all indexes need to be migrated. If the index does not need to be migrated, delete the index before starting the migration. |
   |                                       |                                                                                                                                                                                                                      |
   |                                       | Run the following command to delete the index:                                                                                                                                                                       |
   |                                       |                                                                                                                                                                                                                      |
   |                                       | .. code:: text                                                                                                                                                                                                       |
   |                                       |                                                                                                                                                                                                                      |
   |                                       |    run the db.Collection name.dropIndex(Index name)                                                                                                                                                                  |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
