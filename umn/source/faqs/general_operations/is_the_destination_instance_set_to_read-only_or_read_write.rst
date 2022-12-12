:original_name: drs_04_0021.html

.. _drs_04_0021:

Is the Destination Instance Set to Read-only or Read/Write?
===========================================================

During the migration, the destination instance can be set to read-only or read/write.

-  **Read-only**: During the migration, the destination instance is read-only. After the migration is complete, it restores to the read/write status. This option ensures the integrity and success rate of data migration.
-  **Read/Write**: During the migration, the destination instance can be queried or modified. Data being migrated may be modified when operations are performed or applications are connected. It should be noted that background processes can often generate or modify data, which may result in data conflicts, task faults, and upload failures. Do not select this option if you do not fully understand the risks.

Setting the destination instance to read-only can prevent DDL or DML misoperations from being performed on the databases or tables that are being migrated, improving migration integrity and data consistency.

After a migration task is started, the status of the destination database cannot be changed. After all migration tasks in which the destination database status is set to read-only are complete, the destination database can be read and written.
