:original_name: drs_03_0109.html

.. _drs_03_0109:

Pausing a Migration Task
========================

During migration, if the flow control mode cannot meet the requirements during peak hours, you can pause the migration task.

You can pause the following migration tasks:

-  To the cloud

   -  MySQL->MySQL
   -  MongoDB->DDS

-  From the cloud

   -  MySQL->MySQL
   -  DDS->MongoDB

Prerequisites
-------------

-  You have logged in to the DRS console.
-  The migration task is running properly.

Pausing a Task
--------------

#. In the task list on the **Online Migration Management** page, locate the target task and click **Pause** in the **Operation** column.
#. In the displayed **Pause Task** dialog box, select **Pause log capturing** and click **Yes**.

   .. note::

      -  After the task is paused, the status of the task becomes **Paused**.
      -  After you select **Pause log capturing**, the DRS instance will no longer communicate with the source and destination databases. If the pause duration is too long, the task may fail to be resumed because the logs required by the source database expire. It is recommended that the pause duration be less than or equal to 24 hours.
      -  You can use the resumable transfer function to continue the migration.
