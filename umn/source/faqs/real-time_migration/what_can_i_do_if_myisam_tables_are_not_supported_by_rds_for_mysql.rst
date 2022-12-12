:original_name: drs_04_0032.html

.. _drs_04_0032:

What Can I Do If MyISAM Tables Are Not Supported by RDS for MySQL?
==================================================================

Currently, RDS for MySQL does not support the MyISAM engine due to the following reasons.

-  MyISAM engine tables do not support transactions and support only table-level locks. As a result, read and write operations conflict with each other.
-  MyISAM has a defect in protecting data integrity, which may cause database data damage or even data loss.
-  If data is damaged, MyISAM does not support data restoration provided by RDS for MySQL and requires manual restoration.
-  Data can be transparently migrated from MyISAM to InnoDB, which does not require code modification for tables.

During migration, DRS automatically converts MyISAM to InnoDB. The MyISAM engine table does not support transactions. To ensure data consistency of the MyISAM table, DRS uses primary keys to ensure final data consistency. If you need to migrate MyISAM tables without primary keys, you are advised to start the migration task when no service is running to ensure data consistency.
