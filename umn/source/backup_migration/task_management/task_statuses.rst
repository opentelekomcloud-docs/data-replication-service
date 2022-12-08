:original_name: drs_03_0010.html

.. _drs_03_0010:

Task Statuses
=============

Migration statuses indicate different migration phases.

:ref:`Table 1 <drs_03_0010__table28135752151716>` lists statuses and descriptions of backup migration tasks.

.. _drs_03_0010__table28135752151716:

.. table:: **Table 1** Backup migration task statuses

   +--------------+-----------------------------------------------------------------+
   | Status       | Description                                                     |
   +==============+=================================================================+
   | Restoring    | A backup file is being restored to the destination database.    |
   +--------------+-----------------------------------------------------------------+
   | Successful   | A backup file has been restored to the destination database.    |
   +--------------+-----------------------------------------------------------------+
   | Failed       | A backup file fails to be restored to the destination database. |
   +--------------+-----------------------------------------------------------------+
   | Check failed | A backup file is unavailable.                                   |
   +--------------+-----------------------------------------------------------------+

.. note::

   Deleted migration tasks are not displayed in the status list.
