:original_name: drs_11_0462.html

.. _drs_11_0462:

Cloning a Synchronization Task
==============================

DRS allows you to clone the configuration of existing synchronization tasks. However, tasks in the following status cannot be cloned:

-  Creating
-  Creation failed
-  Configuration
-  Pending start
-  Starting
-  Deleted

You can clone the following data flow types:

-  To the cloud

   -  MySQL->MySQL

-  From the cloud

   -  MySQL->MySQL

.. note::

   -  When a task is cloned, the source and destination database passwords are not cloned. You need to enter the passwords again for the new task.
   -  When you clone a task, the advanced settings for data filtering are not cloned. You need to set the advanced settings for the cloned task again.
   -  Many-to-one task cloning is not supported.
   -  When you clone a task that is being changed, if the change information has been saved to the database, the clone task configuration is the same as the changed configuration.
   -  After a clone task is created, the EIP and private IP address of the new task are different from those of the original task. You may need to configure the network to ensure that the new task can communicate with the source and destination databases.

Prerequisites
-------------

-  You have logged in to the DRS console.
-  A synchronization task has been created.

Procedure
---------

#. On the **Data Synchronization Management** page, select the task to be cloned and click **Clone** in the **Operation** column.
#. In the displayed dialog box, confirm the new task name and click **OK**.
#. After the task is submitted and the task clone is complete, the task status changes to **Configuration**. You can click **Edit** in the **Operation** column, enter the source and destination database passwords again, and edit and start the task.
