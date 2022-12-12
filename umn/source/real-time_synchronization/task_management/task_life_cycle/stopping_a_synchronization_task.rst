:original_name: drs_10_0013.html

.. _drs_10_0013:

Stopping a Synchronization Task
===============================

After the source database and services are migrated to the destination database, you can stop the synchronization task. To prevent data from being overwritten after the source database and services are migrated to the destination database, stop a synchronization task to achieve this goal.

You can stop a task in any of the following statuses:

-  Creating
-  Configuration
-  Pending start
-  Full synchronization
-  Full synchronization failed
-  Incremental synchronization
-  Incremental synchronization failed
-  Paused
-  Fault rectification

.. important::

   -  You are advised to stop the task before performing other operations, such as disconnecting the network between the source database and the synchronization instance. Otherwise, an alarm indicating that the source database cannot be connected will be generated.
   -  For a task in the **Configuration** state, it cannot be stopped if it fails to be configured.
   -  For a task in the **Fault rectification** state, it cannot be stopped if the fault is being rectified.

   -  After a task is stopped, it cannot be retried.

Procedure
---------

#. In the task list on the **Data Synchronization Management** page, locate the target task and click **Stop**.
#. In the displayed dialog box, click **OK**.

   .. note::

      -  If the task status is abnormal (for example, the task fails or the network is abnormal), DRS will select **Forcibly stop task** to preferentially stop the task to reduce the waiting time.
      -  Forcibly stopping a task will release DRS resources. Check whether the synchronization is affected.
      -  To stop the task properly, restore the DRS task first. After the task status becomes normal, click **Stop**.
