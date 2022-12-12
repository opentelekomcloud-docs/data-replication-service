:original_name: drs_11_0075.html

.. _drs_11_0075:

Checking Whether Destination Contains the Configured Database
=============================================================

MySQL > PostgreSQL
------------------

.. table:: **Table 1** Checking whether destination contains the configured database

   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination contains the configured database.                                                                                                                        |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Databases and schemas cannot be migrated. You need to manually create databases and schemas on the destination database. Otherwise, the migration will fail.                     |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: Databases cannot be migrated from MySQL to PostgreSQL.                                                                                                            |
   |                                       |                                                                                                                                                                                  |
   |                                       | Handling suggestion: In the destination database, manually create databases and schemas with the same names as those of the source database.                                     |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The objects to be synchronized already exist in the destination database.                                                                                         |
   |                                       |                                                                                                                                                                                  |
   |                                       | Handling suggestions: Delete the tables to be synchronized from the destination database or select the tables that do not exist in the destination database for synchronization. |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
