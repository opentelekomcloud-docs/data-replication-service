:original_name: drs_16_1155.html

.. _drs_16_1155:

How Do I Check Supplemental Logging of the Source Oracle Database?
==================================================================

In physical standby mode, the Oracle database directly replicates logs from the primary database and does not generate any logs. If the source is an Oracle database, you need to check whether supplemental logging on the primary database meets the requirements to ensure that the task can run properly. The following lists the check and setting methods:

Table level: This setting applies to a specified table.

Database level: This setting applies to the database level.

PK/UI: In addition to the changed columns, the values of the primary key and unique key of each row are recorded.

ALL: Each row of the log records the values of all columns in that row.

.. note::

   DRS incremental synchronization requirements can be met if any of the following checks are passed.

Table-level PK/UI Supplemental Logging Check (Minimum Requirement)
------------------------------------------------------------------

Check whether supplemental logging of the table-level objects to be synchronized meets the requirements.

#. Run the following SQL statement in the source database:

   .. code-block::

      select * from ALL_LOG_GROUPS where (LOG_GROUP_TYPE='UNIQUE KEY LOGGING' or LOG_GROUP_TYPE='PRIMARY KEY LOGGING') and OWNER='Schema name in uppercase' and TABLE_NAME='Table name in uppercase';

   If the table name corresponds to the records whose **LOG_GROUP_TYPE** is **UNIQUE KEY LOGGING** and **PRIMARY KEY LOGGING** in the query result, the DRS incremental synchronization requirements are met.

#. If the requirements are not met, run the following SQL statement to enable table-level PK/UI logging:

   .. code-block::

      alter database add supplemental log data;
      alter table Schema_name.Table_name add supplemental log data(primary key,unique) columns;

All Table-Level Supplemental Log Check
--------------------------------------

Check whether supplemental logging of the table-level objects to be synchronized meets the requirements.

#. Run the following SQL statement in the source database:

   .. code-block::

      select * from ALL_LOG_GROUPS where LOG_GROUP_TYPE='ALL COLUMN LOGGING' and OWNER='Schema_name in uppercase' and TABLE_NAME='Table_name in uppercase';

   If the table name is recorded in the query result, the DRS incremental synchronization requirements can be met.

#. If the requirements are not met, run the following SQL statement to enable all column supplemental logging at the table level:

   .. code-block::

      alter database add supplemental log data;
      alter table Schema_name.Table_name add supplemental log data(all) columns;

Database-level Supplemental Log Check
-------------------------------------

For the database-level objects to be synchronized, check whether supplemental logging meets the requirements.

#. Run the following SQL statement in the source database:

   .. code-block::

      select SUPPLEMENTAL_LOG_DATA_MIN MIN, SUPPLEMENTAL_LOG_DATA_PK PK, SUPPLEMENTAL_LOG_DATA_UI UI, SUPPLEMENTAL_LOG_DATA_ALL ALL_LOG from v$database;

#. Either of the following requirements must be met:

   -  If both **PK** and **UI** are set to **YES**, DRS incremental synchronization requirements can be met.

      If the requirements are not met, run the following SQL statement to enable database-level PK/UI supplemental logging:

      .. code-block::

         alter database add supplemental log data(primary key, unique) columns;

   -  If **ALL_LOG** is set to **YES**, DRS incremental synchronization requirements can be met.

      If the requirements are not met, run the following SQL statement to enable all column supplemental logging at the database level:

      .. code-block::

         alter database add supplemental log data(all) columns;
