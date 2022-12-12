:original_name: drs_14_0006.html

.. _drs_14_0006:

How Do I Export and Import Events and Triggers in Batches?
==========================================================

During the MySQL to MySQL migration, if the migration log indicates that the migration of events and triggers fails after the migration task is complete, you can manually migrate the events and triggers.

This section describes how to export and import events and triggers in batches.

#. Export triggers from the source database in batches.

   a. .. _drs_14_0006__en-us_topic_0000001160467760_li4714141420:

      Run the following statement in the source database to obtain values of **TRIGGER_SCHEMA** and **TRIGGER_NAME**:

      .. code-block:: text

         SELECT TRIGGER_SCHEMA,TRIGGER_NAME  FROM INFORMATION_SCHEMA.TRIGGERS WHERE TRIGGER_SCHEMA in ('DB1','DB2','DB3') order by TRIGGER_NAME;

      In the preceding statements, **DB1**, **DB2**, and **DB3** indicate the databases to be migrated to the destination database.

   b. Run the following statement in the source database to obtain the statement for creating a trigger from the source database from the **SQL Original Statement** field:

      .. code-block:: text

         SHOW CREATE TRIGGER TRIGGER_SCHEMA.TRIGGER_NAME \G;

      In the preceding statement, replace **TRIGGER_SCHEMA** and **TRIGGER_NAME** with the values obtained in :ref:`1.a <drs_14_0006__en-us_topic_0000001160467760_li4714141420>`.

#. Export events from the source database in batches.

   a. .. _drs_14_0006__en-us_topic_0000001160467760_li149211574819:

      Run the following statement in the source database to obtain values of **EVENT_SCHEMA** and **EVENT_NAME**:

      .. code-block:: text

         SELECT EVENT_SCHEMA,EVENT_NAME  FROM INFORMATION_SCHEMA.EVENTS WHERE EVENT_SCHEMA in ('DB1','DB2','DB3') order by EVENT_NAME;

      In the preceding statements, **DB1**, **DB2**, and **DB3** indicate the databases to be migrated to the destination database.

   b. Run the following statement in the source database to obtain the statement for creating an event from the source database from the **SQL Original Statement** field:

      .. code-block:: text

         SHOW CREATE EVENT EVENT_SCHEMA.EVENT_NAME \G;

      In the preceding statement, replace **EVENT_SCHEMA** and **EVENT_NAME** with the values obtained in :ref:`2.a <drs_14_0006__en-us_topic_0000001160467760_li149211574819>`.

#. Import triggers and events.

   Execute the statements for creating triggers and events exported from the source database in the destination database.
