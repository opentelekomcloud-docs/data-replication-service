:original_name: drs_06_0004.html

.. _drs_06_0004:

Task Statuses
=============

:ref:`Table 1 <drs_06_0004__table27183454174548>` lists synchronization task statuses and descriptions.

.. _drs_06_0004__table27183454174548:

.. table:: **Table 1** Task status description

   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status                             | Description                                                                                                                                                        |
   +====================================+====================================================================================================================================================================+
   | Creating                           | A synchronization instance is being created.                                                                                                                       |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Task creation failed               | Failed to create a real-time synchronization instance.                                                                                                             |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Configuration                      | The synchronization instance is successfully created, but the synchronization task is started. You can continue to configure the task.                             |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Pending start                      | The scheduled synchronization task has been delivered to the synchronization instance, waiting for the synchronization instance to start the synchronization task. |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Starting                           | The task is being started.                                                                                                                                         |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Start failed                       | A real-time synchronization task fails to be started.                                                                                                              |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Full synchronization               | A full synchronization task is being performed.                                                                                                                    |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Full synchronization failed        | A full synchronization task fails.                                                                                                                                 |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Incremental synchronization        | An incremental synchronization task is being performed.                                                                                                            |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Incremental synchronization failed | An incremental synchronization task fails.                                                                                                                         |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Modifying task                     | The synchronization object is being modified.                                                                                                                      |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Modifying task failed              | The synchronization object fails to be modified.                                                                                                                   |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Fault rectification                | A synchronization instance is faulty and the system automatically restores the synchronization task.                                                               |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Paused                             | The real-time synchronization task has been paused.                                                                                                                |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Task stopping                      | The synchronization instance and resources used for executing the synchronization task are being released.                                                         |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Completing                         | A synchronization instance and resources are being released.                                                                                                       |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Stopping task failed               | The synchronization instance and resources fail to be released.                                                                                                    |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Completed                          | The task is completed and the synchronization instance is released.                                                                                                |
   +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   -  If a task fails to be created, DRS retains the task for three days by default. After three days, the task automatically ends.
   -  By default, DRS retains a task in the **Configuration** state for three days. After three days, DRS automatically deletes background resources, but the task status remains unchanged. When you reconfigure the task, DRS applies for resources for the task again.
   -  Deleted synchronization tasks are not displayed in the status list.
   -  For a task whose source database is DDM or GaussDB Distributed, the statuses listed above mean statuses of its subtask.
