:original_name: drs_10_0016.html

.. _drs_10_0016:

Modifying Connection Information
================================

A data synchronization task may fail due to the change of the password of the source or destination database. You need to update the information and then retry the synchronization task on the DRS console.

You can modify the following synchronization information:

-  Source database password
-  Destination database password

   .. note::

      After the preceding information is changed, the change takes effect immediately, and the data in the destination database is not cleared.

Prerequisites
-------------

You have logged in to the DRS console.

Procedure
---------

#. On the **Data Synchronization Management** page, click the target synchronization task name in the **Task Name/ID** column.
#. On the **Basic Information** tab, click **Modify Connection Details** in the **Connection Information** area.
#. In the displayed dialog box, change the passwords of the source and destination databases and click **OK**.
