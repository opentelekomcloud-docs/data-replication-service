:original_name: drs_10_0015.html

.. _drs_10_0015:

Mapping Object Names
====================

Data synchronization allows you to synchronize objects (including databases, schemas and tables) in a sources database to the corresponding objects in a destination database. If the synchronization objects in source and destination databases have different names, you can map the source object name to the destination one. The object types that can be mapped include database, schema, and table.

Object name mapping can be used only in the following scenarios:

-  For the first time you select synchronization objects for a data synchronization task.
-  For the first time you add or delete the synchronization object which is not in a mapping relationship.

.. note::

   -  If the destination DB is a type of PostgreSQL, the destination schema name cannot start with **pg\_**. Otherwise, the migration fails.

This section describes how to map objects when configuring a data synchronization task. For details about the mapping relationship, see :ref:`Viewing Synchronization Mapping Information <drs_10_0100>`.

Mapping Databases
-----------------

During real-time synchronization, if the names of source databases to be synchronized are different from those in the destination, you can map the source database names to the destination ones. For example, when synchronizing database A in the source database to database B in the destination database, you need to map database name first.

#. On the **Set Synchronization Task** page, select the database that needs to be mapped from the synchronization objects on the right area and click **Edit**.

#. Changing a database name

   In the displayed dialog box, enter a new database name. The new database name is the name of the database saved in the destination DB instance.

#. Check the result.

   After the database name is changed, the database name before modification and the new database name are displayed. The database mapping is complete.

Mapping Schemas
---------------

A schema is a collection of database objects, including: tables, views, stored procedures, and indexes.

During real-time synchronization, if the names of source schemas to be synchronized are different from those in the destination, you can map the source schema names to the destination ones. For example, you need to synchronize schema A in the source database to schema B in the destination database.

#. On the **Set Synchronization Task** page, select the schema that needs to be mapped from the synchronization objects on the right area and click **Edit**.

#. Edit the schema name.

   In the displayed dialog box, enter a new schema name which is the name to be saved in the destination database.

#. Check the result.

   After the schema name is changed, the schema name before modification and the new schema name are displayed. The schema mapping is complete.

Mapping Tables
--------------

During real-time synchronization, if the names of source tables to be synchronized are different from those in the destination, you can map the source table names to the destination ones. For example, when synchronizing table A in the source database to table B in the destination database you need to map table names first.

#. On the **Set Synchronization Task** page, select the table that needs to be mapped from the synchronization objects on the right area and click **Edit**.

#. Change a table name.

   In the displayed dialog box, enter a new table name. The new table name is the name of the table saved in the destination database.

#. Check the result.

   After the table name is changed, the table name before modification and the new table name are displayed. The table mapping is complete.
