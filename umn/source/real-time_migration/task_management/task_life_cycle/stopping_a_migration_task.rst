:original_name: drs_03_0004.html

.. _drs_03_0004:

Stopping a Migration Task
=========================

After the source database and services are migrated to the destination database, you can stop the migration task. To prevent data from being overwritten after the source database and services are migrated to the destination database, operations on the source database should not be synchronized to the destination database. This section describes how to stop a migration task to achieve this goal.

You can stop a task in any of the following statuses:

-  Creating
-  Configuration
-  Pending start
-  Full migration
-  Full migration failed
-  Incremental migration
-  Incremental migration failed
-  Paused
-  Fault rectification

.. important::

   -  You are advised to stop the task before performing other operations, such as disconnecting the network between the source database and the replication instance. Otherwise, an alarm indicating that the source database cannot be connected will be generated.
   -  For a task in the **Configuration** state, it cannot be stopped if it fails to be configured.
   -  For a task in the **Fault rectification** state, it cannot be stopped if the fault is being rectified.

   -  After a task is stopped, it cannot be resumed.

Prerequisites
-------------

-  You have logged in to the DRS console.
-  A migration task is in progress.

Stopping a Task
---------------

#. On the **Online Migration Management** page, locate the task and click **Stop** in the **Operation** column.
#. In the displayed dialog box, click **OK**.

   .. note::

      -  Generally, triggers and events will be synchronized when you stop the task.
      -  If the task status is abnormal (for example, the task fails or the network is abnormal), DRS will select **Forcibly stop task** to preferentially stop the task to reduce the waiting time.
      -  Forcibly stopping a task will release DRS resources and will not migrate triggers and events. You have to manually migrate triggers and events.
      -  If you need to migrate triggers and events, restore the DRS task first. After the task status becomes normal, you can stop the task.
