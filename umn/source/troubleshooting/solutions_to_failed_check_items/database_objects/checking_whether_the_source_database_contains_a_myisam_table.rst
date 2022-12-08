:original_name: drs_11_0048.html

.. _drs_11_0048:

Checking Whether the Source Database Contains a MyISAM Table
============================================================

MySQL
-----

.. table:: **Table 1** Checking whether the source database contains a MyISAM table

   +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                                   | Whether the source database contains a MyISAM table                                                                                                         |
   +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                                  | If the source database contains a MyISAM table, the migration will fail.                                                                                    |
   +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item to Be Confirmed and Handling Suggestion | Item to be confirmed: The source database contains MyISAM tables that are not supported by the destination database, which may cause the migration to fail. |
   |                                              |                                                                                                                                                             |
   |                                              | Handling suggestion: Convert the tables in the source database to InnoDB tables and try again. Alternatively, contact technical support.                    |
   +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
