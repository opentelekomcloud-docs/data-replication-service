:original_name: drs_11_0053.html

.. _drs_11_0053:

Checking Whether the max_wal_senders Value of the Source Database Is Correctly Configured
=========================================================================================

PostgreSQL Synchronization
--------------------------

.. table:: **Table 1** Checking whether the max_wal_senders value of the source database is correctly configured

   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the **max_wal_senders** value of the source database is correctly configured                                                                                                                                                                      |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | The **max_wal_senders** value of the source database must be greater than the number of used replication slots. Otherwise, the synchronization may fail.                                                                                                  |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The **max_wal_senders** value of the source database is less than or equal to the number of used replication slots.                                                                                                                        |
   |                                       |                                                                                                                                                                                                                                                           |
   |                                       | Handling suggestion: Set **max_wal_senders** to a value greater than the number of used replication slots and restart the database to apply the changes. Run the following command to query the number of used replication slots in the current database: |
   |                                       |                                                                                                                                                                                                                                                           |
   |                                       | .. code:: text                                                                                                                                                                                                                                            |
   |                                       |                                                                                                                                                                                                                                                           |
   |                                       |    select count(1) from pg_replication_slots;                                                                                                                                                                                                             |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
