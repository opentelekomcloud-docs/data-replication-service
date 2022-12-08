:original_name: drs_03_0029.html

.. _drs_03_0029:

Stopping a DR Task
==================

When the DR task is complete or no longer needed, you can stop the DR task. You can stop a task in any of the following statuses:

-  Creating
-  Configuration
-  Initializing
-  Disaster recovery in progress
-  Paused
-  Disaster recovery failed

.. important::

   -  For a task in the **Configuration** state, it cannot be stopped if it fails to be configured.

   -  After a task is stopped, it cannot be reset.

Procedure
---------

#. In the task list on the **Disaster Recovery Management** page, locate the target task and click **Stop** in the **Operation** column.
#. In the displayed dialog box, click **OK**.

   .. note::

      -  If the task status is abnormal (for example, the task fails or the network is abnormal), DRS will select **Forcibly stop task** to preferentially stop the task to reduce the waiting time.
      -  Forcibly stopping a task will release DRS resources. Check whether the synchronization is affected.
      -  To stop the task properly, restore the DRS task first. After the task status becomes normal, click **Stop**.
