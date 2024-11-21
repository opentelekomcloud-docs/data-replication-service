:original_name: drs_03_1138.html

.. _drs_03_1138:

Modifying Connection Information
================================

A data DR task may fail due to the password change of the service or DR database. You need to update the information and then retry the DR task on the DRS console.

You can modify the following information:

-  Source database password
-  Destination database password

   .. note::

      After the preceding information is changed, the change takes effect immediately, and the data in the DR database is not cleared.

Prerequisites
-------------

You have logged in to the DRS console.

Procedure
---------

#. On the **Disaster Recovery Management** page, click the target DR task in the **Task Name/ID** column.
#. On the **Basic Information** page, click **Modify Connection Details** in the **DR Information** area.
#. In the displayed dialog box, change the passwords of the source and destination databases and click **OK**.
