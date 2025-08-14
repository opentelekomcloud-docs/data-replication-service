:original_name: drs_11_0010.html

.. _drs_11_0010:

Checking Whether the Destination Database Has Sufficient Storage Space
======================================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the destination database has sufficient storage space

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination database has sufficient storage space                                                                                                          |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the destination database has sufficient storage space. If storage space is insufficient, the migration will fail.                                        |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: This item cannot be checked because the source database fails to be connected.                                                                          |
   |                                       |                                                                                                                                                                        |
   |                                       | Handling suggestion: Check whether the source database is connected.                                                                                                   |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Insufficient user permissions                                                                                                                           |
   |                                       |                                                                                                                                                                        |
   |                                       | Handling suggestion: Check whether the database user permissions meet the migration requirements.                                                                      |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The destination database does not have sufficient storage space (at least 2.5 times the size of the source database).                                   |
   |                                       |                                                                                                                                                                        |
   |                                       | Handling suggestion: Scale up or clean up the destination database storage space. If you clean up the storage space, you will obtain more space within 2 to 3 minutes. |
   |                                       |                                                                                                                                                                        |
   |                                       | .. note::                                                                                                                                                              |
   |                                       |                                                                                                                                                                        |
   |                                       |    It is recommended that the size of the destination database disk be set to the smaller value of the following two values:                                           |
   |                                       |                                                                                                                                                                        |
   |                                       |    #. 2.5 times the size of the data to be migrated in the source database.                                                                                            |
   |                                       |    #. The size of the data to be migrated in the source database plus 200 GB.                                                                                          |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                                                               |
   |                                       |                                                                                                                                                                        |
   |                                       | Handling suggestion: Contact technical support.                                                                                                                        |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

PostgreSQL Synchronization
--------------------------

.. table:: **Table 2** Checking whether the destination database has sufficient storage space

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination database has sufficient storage space                                                                                                          |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the destination database has sufficient storage space. If storage space is insufficient, the synchronization will fail.                                  |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: This item cannot be checked because the source database fails to be connected.                                                                          |
   |                                       |                                                                                                                                                                        |
   |                                       | Handling suggestion: Check whether the source database is connected.                                                                                                   |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The destination database does not have sufficient storage space (at least 1.5 times the size of the source database).                                   |
   |                                       |                                                                                                                                                                        |
   |                                       | Handling suggestion: Scale up or clean up the destination database storage space. If you clean up the storage space, you will obtain more space within 2 to 3 minutes. |
   |                                       |                                                                                                                                                                        |
   |                                       | .. note::                                                                                                                                                              |
   |                                       |                                                                                                                                                                        |
   |                                       |    It is recommended that the size of the destination database disk be set to the smaller value of the following two values:                                           |
   |                                       |                                                                                                                                                                        |
   |                                       |    #. 1.5 times the size of the data to be migrated in the source database.                                                                                            |
   |                                       |    #. The size of the data to be migrated in the source database plus 200 GB.                                                                                          |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                                                               |
   |                                       |                                                                                                                                                                        |
   |                                       | Handling suggestion: Contact technical support.                                                                                                                        |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

MongoDB Migration
-----------------

.. table:: **Table 3** Checking whether the destination database has sufficient storage space

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination database has sufficient storage space                                                                                                          |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the destination database has sufficient storage space. If storage space is insufficient, the migration will fail.                                        |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: This item cannot be checked because the source database fails to be connected.                                                                          |
   |                                       |                                                                                                                                                                        |
   |                                       | Handling suggestion: Check whether the source database is connected.                                                                                                   |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The destination database does not have sufficient storage space (at least 1.5 times the size of the source database).                                   |
   |                                       |                                                                                                                                                                        |
   |                                       | Handling suggestion: Scale up or clean up the destination database storage space. If you clean up the storage space, you will obtain more space within 2 to 3 minutes. |
   |                                       |                                                                                                                                                                        |
   |                                       | .. note::                                                                                                                                                              |
   |                                       |                                                                                                                                                                        |
   |                                       |    It is recommended that the size of the destination database disk be set to the smaller value of the following two values:                                           |
   |                                       |                                                                                                                                                                        |
   |                                       |    #. 1.5 times the size of the data to be migrated in the source database.                                                                                            |
   |                                       |    #. The size of the data to be migrated in the source database plus 200 GB.                                                                                          |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                                                               |
   |                                       |                                                                                                                                                                        |
   |                                       | Handling suggestion: Contact technical support.                                                                                                                        |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
