:original_name: drs_03_1136.html

.. _drs_03_1136:

Cloning a Migration Task
========================

DRS allows you to quickly clone the configuration of an existing migration task. However, tasks in the following status cannot be cloned:

-  Creating
-  Creation failed
-  Configuration
-  Pending start
-  Starting
-  Deleted

You can clone the following migration tasks:

-  To the cloud

   -  MongoDB -> DDS

-  Out of the cloud

   -  DDS -> MongoDB

.. note::

   -  When a task is cloned, the source and destination database passwords are not cloned. You need to enter the passwords again for the new task.
   -  After a clone task is created, the EIP and private IP address of the new task are different from those of the original task. You may need to configure the network to ensure that the new task can communicate with the source and destination databases.

Prerequisites
-------------

-  You have logged in to the DRS console.
-  A migration task has been created.

Procedure
---------

#. On the **Online Migration Management** page, select the task to be cloned and click **Clone** in the **Operation** column.
#. In the displayed dialog box, confirm the new task name and click **OK**.
#. After the task is submitted and the task clone is complete, the task status changes to **Configuration**. You can click **Edit** in the **Operation** column, enter the source and destination database passwords again, and edit and start the task.
