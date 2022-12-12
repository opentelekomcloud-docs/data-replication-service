:original_name: drs_11_0018.html

.. _drs_11_0018:

Checking Whether the Source Database server_id Meets the Incremental Migration Requirements
===========================================================================================

MySQL
-----

.. table:: **Table 1** Checking whether the source database server_id meets the incremental migration requirements

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database **server_id** meets the incremental migration requirements                                                                                                                     |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the source database **server_id** meets the incremental migration requirements.                                                                                                              |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: This item cannot be checked because the source database failed to be connected.                                                                                                             |
   |                                       |                                                                                                                                                                                                            |
   |                                       | Handling suggestion: Check whether the source database is connected.                                                                                                                                       |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Insufficient user permissions                                                                                                                                                               |
   |                                       |                                                                                                                                                                                                            |
   |                                       | Handling suggestion: Check whether the database user permissions meet the migration requirements.                                                                                                          |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The source database **server_id** does not meet the incremental migration requirements.                                                                                                     |
   |                                       |                                                                                                                                                                                                            |
   |                                       | Handling suggestion:                                                                                                                                                                                       |
   |                                       |                                                                                                                                                                                                            |
   |                                       | Run the following command to modify the **server_id** value:                                                                                                                                               |
   |                                       |                                                                                                                                                                                                            |
   |                                       | **set global server_id=n**                                                                                                                                                                                 |
   |                                       |                                                                                                                                                                                                            |
   |                                       | The value **n** indicates the source database server_id. If the source database version is MySQL 5.6, the value **n** ranges from 2 to 4294967296. Otherwise, the value **n** ranges from 1 to 4294967296. |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                                                                                                   |
   |                                       |                                                                                                                                                                                                            |
   |                                       | Handling suggestion: Contact technical support.                                                                                                                                                            |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
