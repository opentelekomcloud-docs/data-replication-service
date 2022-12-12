:original_name: drs_11_0463.html

.. _drs_11_0463:

Checking Whether the ChangeStream API of the source DB instance is available
============================================================================

MongoDB-to-DDS Migration
------------------------

.. table:: **Table 1** Checking whether the ChangeStream API of the source DB instance is available

   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the ChangeStream API of the source DB instance is available                                                                                                                                     |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the ChangeStream API of the source database is available.                                                                                                                                 |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The source database cannot use the ChangeStream API.                                                                                                                                     |
   |                                       |                                                                                                                                                                                                         |
   |                                       | Handling suggestion:                                                                                                                                                                                    |
   |                                       |                                                                                                                                                                                                         |
   |                                       | #. Check whether the source database version is MongoDB 4.0 or later.                                                                                                                                   |
   |                                       |                                                                                                                                                                                                         |
   |                                       | #. Check whether the WiredTiger storage engine is enabled for the source database. If not, you are advised to create a DRS task and select the oplog mode. Run the following command (on a shard node): |
   |                                       |                                                                                                                                                                                                         |
   |                                       |    .. code:: text                                                                                                                                                                                       |
   |                                       |                                                                                                                                                                                                         |
   |                                       |       db.serverStatus().storageEngine.name;                                                                                                                                                             |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The source database cannot use the ChangeStream API.                                                                                                                                     |
   |                                       |                                                                                                                                                                                                         |
   |                                       | Handling suggestion: Check whether the source database version is DDS 4.0 or later. If not, upgrade the source database to DDS 4.0 or later.                                                            |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
