:original_name: drs_16_1133.html

.. _drs_16_1133:

How Do I Solve the Table Bloat Issue?
=====================================

In the full migration phase, DRS uses the row-level parallel migration mode to ensure migration performance and transmission stability. If the source database data is compact, table bloat may occur after data is migrated to the RDS MySQL database. As a result, the disk space required is much greater than that of the source database. In this case, you can run the following command in the destination database to free up the space:

.. code-block:: text

   optimize table table_name

.. note::

   The OPTIMIZE TABLE command locks tables. Do not run this command when you operate table data. Otherwise, services may be affected.
