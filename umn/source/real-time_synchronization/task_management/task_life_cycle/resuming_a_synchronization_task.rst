:original_name: drs_10_0400.html

.. _drs_10_0400:

Resuming a Synchronization Task
===============================

A fault may occur during the synchronization due to external factors, such as insufficient storage space. After the fault is rectified based on the synchronization log information, you can resume the synchronization.

You can resume synchronization tasks in any of the following statuses:

-  Synchronization failed
-  Paused

   .. note::

      -  If the synchronization task fails due to non-network problems, the system will automatically resume the task three times by default. If the failure persists, you can resume the task manually.
      -  If the synchronization fails due to network problems, the system will automatically resume the task until the synchronization is restored.

Prerequisites
-------------

You have logged in to the DRS console.

Method 1
--------

In the task list on the **Data Synchronization Management** page, locate the target task and click **Resume** in the **Operation** column.

Method 2
--------

#. On the **Data Synchronization Management** page, click the target synchronization task name in the **Task Name/ID** column.
#. On the displayed page, click the **Synchronization Progress** tab, and click **Resume** in the upper left corner.

Resume Tasks
------------

#. On the **Data Synchronization Management** page, select the tasks to be resumed.
#. Click **Batch Operations** in the upper left corner and choose **Resume**.
#. In the displayed dialog box, confirm the task information and click **Yes**.
