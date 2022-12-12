:original_name: drs_10_0009.html

.. _drs_10_0009:

Editing Synchronization Objects
===============================

This section describes how to change synchronization objects in a synchronization task. After a data synchronization task is created, you can change synchronization objects by adding or deleting databases and tables to be synchronized during the incremental synchronization.

Prerequisites
-------------

You have logged in to the DRS console.

Method 1
--------

#. On the **Data Synchronization Management** page, locate the target synchronization task and click **Edit** in the **Operation** column.

#. .. _drs_10_0009__li443419465279:

   On the **Set Synchronization Task** page, change the objects to be synchronized and click **Next**.

#. On the **Check Task** page, check the synchronization task.

   -  If any check fails, review the cause and rectify the fault. After the fault is rectified, click **Check Again**.
   -  If all check items are successful, click **Next**.

      .. note::

         You can proceed to the next step only when all checks are successful. If there are any items that require confirmation, view and confirm the details first before proceeding to the next step.

#. .. _drs_10_0009__li0155332161410:

   In the synchronization task list on the **Data Synchronization Management** page, the current task status is **Incremental synchronization**, and a subtask in the **Modifying task** status is generated. After the subtask change is complete, incremental synchronization is performed for the edited synchronization objects.

Method 2
--------

#. On the **Data Synchronization Management** page, click the target synchronization task.
#. On the displayed page, click the **Synchronization Mapping** tab and click **Edit** to the right of the synchronization object.
#. Perform :ref:`2 <drs_10_0009__li443419465279>` to :ref:`4 <drs_10_0009__li0155332161410>` from method 1.
