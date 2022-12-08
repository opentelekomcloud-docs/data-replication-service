:original_name: drs_11_0050.html

.. _drs_11_0050:

Checking Whether the Destination Database Has a Read Replica
============================================================

MySQL
-----

.. table:: **Table 1** Checking whether the destination database has a read replica

   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination database has a read replica                                                                                          |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the destination database has read replicas. If the destination database has read replicas, the incremental migration may fail. |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: In an incremental migration, the destination database cannot have read replicas.                                              |
   |                                       |                                                                                                                                              |
   |                                       | Handling suggestion: Delete the read replicas from the destination database. After the migration is complete, create read replicas.          |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
