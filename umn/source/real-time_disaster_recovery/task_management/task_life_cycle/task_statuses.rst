:original_name: drs_02_0025.html

.. _drs_02_0025:

Task Statuses
=============

DR statuses indicate different DR phases.

:ref:`Table 1 <drs_02_0025__table27183454174548>` lists DR task statuses and descriptions.

.. _drs_02_0025__table27183454174548:

.. table:: **Table 1** Task status and description

   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Status                        | Description                                                                                       |
   +===============================+===================================================================================================+
   | Creating                      | A DR instance is being created for DRS.                                                           |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Configuration                 | A DR instance is created, but the DR task is not started. You can continue to configure the task. |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Pending start                 | A scheduled DR task is created for the DR instance, waiting to be started.                        |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Starting                      | A DR task is starting.                                                                            |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Start failed                  | A real-time DR task fails to be created.                                                          |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Initialization                | Full data from the service database to the DR database is being initialized.                      |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Initialization completed      | The DR task has been initialized.                                                                 |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Disaster recovery in progress | Incremental data from the service database is being synchronized to the DR database.              |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Switching over                | The primary/standby switchover of a DR task is being performed.                                   |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Paused                        | The real-time DR synchronization task is paused.                                                  |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Disaster recovery failed      | A DR task fails during the disaster recovery.                                                     |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Task stopping                 | A DR instance and resources are being released.                                                   |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Completing                    | A DR instance and resources are being released.                                                   |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Stopping task failed          | Instances and resources used by the DR task fail to be released.                                  |
   +-------------------------------+---------------------------------------------------------------------------------------------------+
   | Completed                     | The DR instance used by a DR task is released successfully.                                       |
   +-------------------------------+---------------------------------------------------------------------------------------------------+

.. note::

   -  If a task fails to be created, DRS retains the task for three days by default. After three days, the task automatically ends.
   -  Deleted DR tasks are not displayed in the status list.
