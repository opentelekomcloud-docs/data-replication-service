:original_name: drs_14_0002.html

.. _drs_14_0002:

How Can I Migrate Databases or Tables Whose Names Contain Uppercase Letters?
============================================================================

Scenarios
---------

When the value of source database parameter **lower_case_table_names** is set to **1**, the databases or tables whose names contain uppercase letters cannot be migrated.

Possible Cause
--------------

When the value of **lower_case_table_names** in the source database is **1**, the MySQL engine converts the database name or table name into lowercase letters. In this case, the database or table may not be found, resulting in query failure. Simply, if the value of **lower_case_table_names** is **1**, the database or table containing uppercase letters may be inaccessible.

Solutions
---------

Two solutions are provided as follows:

Solution 1
----------

Change the value of **lower_case_table_names** in the source database to **0** (case-sensitive) and ensure that the value of this parameter in the source database is the same as that in the destination database.

Solution 2
----------

If the value of **lower_case_table_names** cannot be changed permanently, change the value to **0**, and then perform the following operations:

-  For a table, you can use the following statement to convert the table name to lowercase:

   .. code-block:: text

      alter table `BigTab` rename to `bigtab`

-  For a database, you need to export the database data, change the database name from uppercase to lowercase, and then import the data.

.. caution::

   After changing the database name or table name, you need to maintain the permission consistency without affecting application access.

Method 3
--------

Do not migrate the databases or tables that contain uppercase letters.
