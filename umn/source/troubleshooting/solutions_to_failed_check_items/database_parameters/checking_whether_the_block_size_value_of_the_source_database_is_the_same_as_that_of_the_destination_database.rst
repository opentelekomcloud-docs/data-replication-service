:original_name: drs_11_0063.html

.. _drs_11_0063:

Checking Whether the BLOCK_SIZE Value of the Source Database Is the Same as That of the Destination Database
============================================================================================================

PostgreSQL Synchronization
--------------------------

.. table:: **Table 1** Checking whether the BLOCK_SIZE value of the source database is the same as that of the destination database

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the **BLOCK_SIZE** value of the source database is the same as that of the destination database                                                     |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | The **BLOCK_SIZE** value of the destination database must be greater than or equal to that of the source database. Otherwise, the synchronization may fail. |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The **BLOCK_SIZE** value of the destination database is less than that of the source database.                                               |
   |                                       |                                                                                                                                                             |
   |                                       | Handling suggestion:                                                                                                                                        |
   |                                       |                                                                                                                                                             |
   |                                       | -  Use the destination database whose **BLOCK_SIZE** value is greater than or equal to that of the source database.                                         |
   |                                       | -  Use the source database whose **BLOCK_SIZE** value is less than or equal to the value of destination database **BLOCK_SIZE**.                            |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
