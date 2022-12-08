:original_name: drs_10_0010.html

.. _drs_10_0010:

Editing a Synchronization Task
==============================

For a synchronization task that has been created but not started, DRS allows you to edit the configuration information of the task, including the source and destination database details. For synchronization tasks in the following statuses, you can edit and submit the tasks again.

-  Creating
-  Configuration

   .. note::

      For an incremental synchronization task, DRS allows you to modify synchronization objects. For details, see :ref:`Editing Synchronization Objects <drs_10_0009>`.

Prerequisites
-------------

You have logged in to the DRS console.

Method 1
--------

#. In the task list on the **Data Synchronization Management** page, locate the target task and click **Edit** in the **Operation** column.

#. .. _drs_10_0010__li105671010104417:

   On the **Configure Source and Destination Databases** page, enter information about the source and destination databases and click **Next**.

#. On the **Set Synchronization Task** page, select synchronization objects and click **Next**.

#. On the **Check Task** page, check the synchronization task.

#. On the **Confirm Task** page, specify **Start Time**, confirm that the configured information is correct, and click **Next**.

#. .. _drs_10_0010__li620112563620:

   After the task is submitted, you can view and manage it on the **Data Synchronization Management** page.

Method 2
--------

#. On the **Data Synchronization Management** page, click the target synchronization task.
#. On the displayed page, click **edit this task** to go to the **Configure Source and Destination Databases** page.
#. Perform :ref:`2 <drs_10_0010__li105671010104417>` to :ref:`6 <drs_10_0010__li620112563620>` from method 1.
