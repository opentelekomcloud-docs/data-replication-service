:original_name: drs_16_0120.html

.. _drs_16_0120:

Constraints and Operation Suggestions on Many-to-One Scenario
=============================================================

DRS supports many-to-one scenarios during migration of different types of instances and tables to suit your service requirements.

Operation Suggestions
---------------------

-  To ensure that there is sufficient space during task creation, you are advised to calculate the total data volume of the source database and plan how to allocate the disk space of the destination instance. The remaining disk space must be greater than the total data volume of the source database. For example, if the data volume of source system1 is 1 GB, the data volume of source system2 is 3 GB, and the data volume of source system3 is 6 GB, the remaining disk space of the destination instance must be greater than 10 GB.
-  To improve the performance of the destination MySQL database, you are advised to use the **Save Change** function to configure common parameters (except **max_connections**). For performance parameters, you need to manually change the parameter values based on the specifications of the destination database.
-  When you create a many-to-one synchronization task, the task created later may block the task created earlier. This is because each synchronization task involves index creation. When an index is created, a schema lock may occur on the destination database, which blocks the synchronization of other tables in the schema. As a result, the previously created tasks cannot be synchronized. To avoid this problem, you are advised to set **Start Time** to **Start at a specified time** to start a task during off-peak hours.
-  For many-to-one synchronization tasks that involve the synchronization of the same table, DDL operations cannot be performed on source databases. Otherwise, all synchronization tasks fail.

Many-to-One Data Migration
--------------------------

Data migration aims to migrate the entire database. Multiple databases can be migrated at the instance level. Databases with the same name in the source system cannot be migrated and database name mapping is not supported.


.. figure:: /_static/images/en-us_image_0000001758549529.png
   :alt: **Figure 1** Many-to-one data migration

   **Figure 1** Many-to-one data migration

Flow Chart
----------

When creating a task, ensure that the second task is created after the first task has entered the full migration state.


.. figure:: /_static/images/en-us_image_0000001710470616.png
   :alt: **Figure 2** Flow chart

   **Figure 2** Flow chart
