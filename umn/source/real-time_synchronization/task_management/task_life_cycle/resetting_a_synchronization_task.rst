:original_name: drs_10_0300.html

.. _drs_10_0300:

Resetting a Synchronization Task
================================

During real-time synchronization, you can reset the synchronization tasks in one of the following statuses so that you do not need to configure the tasks again.

-  Paused
-  Incremental synchronization failed

You can reset the following DRS tasks:

-  To the cloud

   -  MySQL->MySQL
   -  PostgreSQL->PostgreSQL

-  From the cloud

   -  MySQL->MySQL

.. note::

   -  For a many-to-one synchronization task, only the parent task can be reset.
   -  For a MySQL many-to-one synchronization task, only the subtask can be reset.
   -  Resetting a task does not clear the destination database. You can determine whether to clear the destination database based on your service requirements. After the task is reset, a full synchronization is performed again. You do not need to configure the task again.

Prerequisites
-------------

You have logged in to the DRS console.

Method 1
--------

#. In the task list on the **Data Synchronization Management** page, locate the target task and click **Reset** in the **Operation** column.

#. .. _drs_10_0300__li1764125135215:

   In the displayed dialog box, check the synchronization task again.

   .. note::

      If a many-to-one synchronization task fails to be reset, click the name of the failed subtask in the failure details to view the failure cause of the task.

#. .. _drs_10_0300__li1436312473210:

   After the check is complete and the check success rate is 100%, click **Start** to submit the synchronization task again.

Method 2
--------

#. On the **Data Synchronization Management** page, click the target synchronization task name in the **Task Name/ID** column.
#. On the displayed page, click the **Synchronization Progress** tab, and click **Reset** in the upper left corner.
#. Perform :ref:`2 <drs_10_0300__li1764125135215>` to :ref:`3 <drs_10_0300__li1436312473210>` from method 1.
