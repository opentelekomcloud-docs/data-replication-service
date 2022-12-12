:original_name: drs_03_1135.html

.. _drs_03_1135:

Modifying Connection Information
================================

During the migration, you may change the password of the source or destination database. As a result, the migration task fails. In this case, you need to change the password on the DRS console and resume the task.

You can modify the following information:

-  Source database password
-  Destination database password

   .. note::

      After the preceding information is changed, the change takes effect immediately, and the data in the destination database is not cleared.

Prerequisites
-------------

You have logged in to the DRS console.

Procedure
---------

#. On the **Online Migration Management** page, click the target migration task name in the **Task Name/ID** column.
#. On the **Basic Information** tab, click **Modify Connection Details** in the **Migration Information** area.
#. In the displayed dialog box, change the passwords of the source and destination databases and click **OK**.
