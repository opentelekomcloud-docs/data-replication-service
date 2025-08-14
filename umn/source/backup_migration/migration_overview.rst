:original_name: drs_offline_migration.html

.. _drs_offline_migration:

Migration Overview
==================

It often becomes necessary to hide the real IP address of your database for the sake of security. Migrating data through direct connections is an option, but costly. DRS supports backup migration, which allows you to export data from your source database for backup and upload the backup files to OBS. Then, you can restore the backup files to the destination database to complete the migration. Using this method, data migration can be realized without exposing your source databases.

You can use backup migration when you want to migrate on-premises databases to the cloud.

Without connecting to your sources, DRS can help you complete data migration.

Supported Database Types
------------------------

:ref:`Table 1 <drs_offline_migration__table1993916116112>` lists the source database and destination database types supported by DRS in backup migration.

.. _drs_offline_migration__table1993916116112:

.. table:: **Table 1** Migration schemes

   +------------------------------------------------------------------+--------------------+------------------------------------------------------------+
   | Backup File                                                      | Destination DB     | Documentation                                              |
   +==================================================================+====================+============================================================+
   | Full backup file of RDS for SQL Server                           | RDS for SQL Server | :ref:`Creating an RDS Backup Migration Task <drs_02_0010>` |
   +------------------------------------------------------------------+--------------------+------------------------------------------------------------+
   | Backup files of on-premises and other cloud Microsoft SQL Server |                    | :ref:`Creating a Backup Using OBS Buckets <drs_02_0009>`   |
   +------------------------------------------------------------------+--------------------+------------------------------------------------------------+
