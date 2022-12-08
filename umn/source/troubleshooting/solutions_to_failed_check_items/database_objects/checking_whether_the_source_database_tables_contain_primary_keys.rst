:original_name: drs_15_0020.html

.. _drs_15_0020:

Checking Whether the Source Database Tables Contain Primary Keys
================================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the source database tables contain primary keys

   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                                   | Whether the source database tables contain primary keys                                                                                                                                                                                                             |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                                  | If tables to be migrated in the source database do not contain primary keys, the migration may fail.                                                                                                                                                                |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item to Be Confirmed and Handling Suggestion | Item to be confirmed: The tables to be migrated in the source database do not contain primary keys.                                                                                                                                                                 |
   |                                              |                                                                                                                                                                                                                                                                     |
   |                                              | Handling suggestion: Create a primary key for the table. If the table does not have a primary key to uniquely identify every row and the network connection is unstable, the data in the destination database may be inconsistent with that in the source database. |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
