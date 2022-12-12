:original_name: drs_11_0069.html

.. _drs_11_0069:

Checking Whether the Shard Key Can Be Obtained from the Source Database
=======================================================================

MongoDB Migration
-----------------

.. table:: **Table 1** Checking whether the shard keys can be obtained from the source database

   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the shard keys can be obtained from the source database                                                                                        |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the destination database user permissions meet the migration requirements. If the permissions are insufficient, the migration will fail. |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Item to be confirmed: The source database is a replica set but the shard keys have not been configured in the destination database.                    |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Item to be confirmed: The source database type is unknown, and the shard keys have not been configured in the destination database.                    |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Item to be confirmed: The source database contains collections that do not have shard keys configured.                                                 |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
