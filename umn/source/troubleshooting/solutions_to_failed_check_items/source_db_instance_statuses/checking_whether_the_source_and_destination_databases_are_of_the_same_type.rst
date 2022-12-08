:original_name: drs_11_0046.html

.. _drs_11_0046:

Checking Whether the Source and Destination Databases Are of the Same Type
==========================================================================

MongoDB Migration
-----------------

.. table:: **Table 1** Checking whether the source and destination databases are of the same type

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source and destination databases are of the same type                                                             |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the source and destination databases are of the same type. If they are of different types, the migration fails. |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The destination database is a cluster but the source database is a replica set.                                |
   |                                       |                                                                                                                               |
   |                                       | Handling suggestion: Change the type of the source or destination database.                                                   |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The destination database is a replica set but the source database is a cluster.                                |
   |                                       |                                                                                                                               |
   |                                       | Handling suggestion: Change the type of the source or destination database.                                                   |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
