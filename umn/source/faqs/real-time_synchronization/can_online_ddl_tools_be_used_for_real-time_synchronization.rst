:original_name: drs_16_1124.html

.. _drs_16_1124:

Can Online DDL Tools Be Used for Real-time Synchronization?
===========================================================

During table-level incremental synchronization from MySQL to MySQL, you can use Online DDL tools to add or delete columns. Pay attention to the following when using Online DDL:

-  The DRS synchronization mechanism conflicts with the tool. Do not select **Incremental DDLs** when selecting synchronization objects on the **Set Synchronization Task** page.
-  Before using Online DDL tools to add columns, perform the corresponding operations in the destination database and then in the source database.
-  When using Online DDL tools to delete columns, perform the corresponding operation in the source database and then in the destination database.

Common online DDL tools:

-  pt-online-schema-change
-  gh-ost
