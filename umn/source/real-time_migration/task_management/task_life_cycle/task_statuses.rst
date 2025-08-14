:original_name: drs_03_0001.html

.. _drs_03_0001:

Task Statuses
=============

Migration statuses indicate different migration phases.

:ref:`Table 1 <drs_03_0001__table27183454174548>` lists statuses and descriptions of online migration tasks.

.. _drs_03_0001__table27183454174548:

.. table:: **Table 1** Task status and description

   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status                       | Description                                                                                                                                    |
   +==============================+================================================================================================================================================+
   | Creating                     | A replication instance is being created for DRS.                                                                                               |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Task creation failed.        | Failed to create a replication instance for real-time migration.                                                                               |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Configuring                  | A replication instance is created, but the migration task is not started. You can continue to configure the task.                              |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Pending start                | The scheduled migration task has been delivered to the replication instance, waiting for the replication instance to start the migration task. |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Starting                     | A migration task is being started.                                                                                                             |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Start failed                 | Failed to start a real-time migration task.                                                                                                    |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Full migration               | A full migration task is being performed.                                                                                                      |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Full migration failed        | Failed to perform a full migration task.                                                                                                       |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Incremental migration        | An incremental migration task is being performed.                                                                                              |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Incremental migration failed | Failed to perform an incremental migration task.                                                                                               |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Fault rectification          | A replication instance is faulty and the system automatically restores the migration task.                                                     |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Paused                       | A real-time migration task is paused.                                                                                                          |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Stopping                     | The replication instance and resources used for executing the migration task are being released.                                               |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Completing                   | A replication instance and resources are being released.                                                                                       |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Stopping task failed         | Failed to release the replication instance and resources used by the migration task.                                                           |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Completed                    | The task is completed and the replication instance is released.                                                                                |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   -  If a task fails to be created, DRS retains the task for three days by default. After three days, the task automatically ends.
   -  By default, DRS retains a task in the **Configuration** state for three days. After three days, DRS automatically deletes background resources, but the task status remains unchanged. When you reconfigure the task, DRS applies for resources for the task again.
   -  Deleted migration tasks are not displayed in the status list.
   -  For a task whose source database is DDM, the statuses listed above mean statuses of its subtask.
