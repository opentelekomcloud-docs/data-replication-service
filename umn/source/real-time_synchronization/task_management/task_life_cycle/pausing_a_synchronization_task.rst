:original_name: drs_03_0110.html

.. _drs_03_0110:

Pausing a Synchronization Task
==============================

DRS allows you to pause real-time synchronization tasks.

The following tasks can be paused during incremental synchronization:

-  To the cloud

   -  MySQL->MySQL
   -  PostgreSQL->PostgreSQL
   -  Oracle->PostgreSQL

-  From the cloud

   -  MySQL->MySQL
   -  MySQL->Kafka

-  Self-built -> Self-built

   -  MySQL->Kafka

In addition, the following tasks can be paused during full synchronization:

-  MySQL->MySQL

Prerequisites
-------------

-  You have logged in to the DRS console.

Pausing a Task
--------------

#. In the task list on the **Online Synchronization Management** page, locate the target task and click **Pause** in the **Operation** column.
#. In the displayed **Pause Task** dialog box, select **Pause log capturing** and click **Yes**.

   .. note::

      -  After the task is paused, the status of the task becomes **Paused**.
      -  After you select **Pause log capturing**, the DRS instance will no longer communicate with the source and destination databases. If the pause duration is too long, the task may fail to be resumed because the logs required by the source database expire. It is recommended that the pause duration be less than or equal to 24 hours.

Pausing Tasks
-------------

#. On the **Data Synchronization Management** page, select the tasks to be paused.
#. Click **Batch Operations** in the upper left corner and choose **Pause**.
#. In the displayed dialog box, confirm the task information and click **Yes**.
