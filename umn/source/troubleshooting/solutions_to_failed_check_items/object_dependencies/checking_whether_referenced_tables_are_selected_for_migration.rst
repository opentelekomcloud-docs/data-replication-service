:original_name: drs_11_0222.html

.. _drs_11_0222:

Checking Whether Referenced Tables Are Selected for Migration
=============================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the tables referenced by the foreign key in the table to be migrated are selected for migration.

   +----------------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | Check Item                                   | Whether the tables referenced by the foreign key in the table to be migrated are selected for migration.        |
   +----------------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | Description                                  | The tables referenced by the foreign key in the table to be migrated are not selected for migration.            |
   +----------------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | Item to Be Confirmed and Handling Suggestion | Failure cause: Tables referenced by the foreign key in the table to be migrated are not selected for migration. |
   |                                              |                                                                                                                 |
   |                                              | Handling suggestion: Select the referenced tables.                                                              |
   +----------------------------------------------+-----------------------------------------------------------------------------------------------------------------+
