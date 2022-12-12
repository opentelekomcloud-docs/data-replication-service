:original_name: drs_11_0117.html

.. _drs_11_0117:

Checking Whether the Source Database Tables Use Storage Engines Not Supported by the Destination Database
=========================================================================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the source database tables use storage engines not supported by the destination database

   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                                   | Whether the source database tables use storage engines not supported by the destination database                                                  |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                                  | Check whether the source database tables use storage engines not supported by the destination database. If yes, the migration fails.              |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item to Be Confirmed and Handling Suggestion | Failure cause: The source database tables use the storage engines that are not supported by the destination database.                             |
   |                                              |                                                                                                                                                   |
   |                                              | Handling suggestion: Go back to the previous page and deselect the tables that use the storage engines not supported by the destination database. |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
