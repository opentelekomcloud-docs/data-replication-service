:original_name: drs_03_1131.html

.. _drs_03_1131:

Forcibly Stopping Synchronization from GaussDB Distributed
==========================================================

This section describes how to delete streaming replication slots of the source distributed GaussDB database after an incremental or a full+incremental synchronization task is forcibly stopped.

Prerequisites
-------------

Common users do not have the permission to perform EXECUTE DIRECT. To delete streaming replication slots, contact GaussDB O&M personnel.

Procedure
---------

#. Log in to each primary DN node of the distributed GaussDB instance as the user used when you tested the connectivity between the DRS instance and the distributed GaussDB instance.

#. .. _drs_03_1131__li4276143622720:

   Run the following statement to query the streaming replication slot name of the database object selected for the synchronization task:

   .. code-block::

      select slot_name from pg_replication_slots where database = 'database';

   .. important::

      In the preceding command, *database* indicates the database selected in the synchronization task.

#. Run the following statement to delete the streaming replication slot:

   .. code-block::

      select * from pg_drop_replication_slot('slot_name');

   .. important::

      In the preceding command, *slot_name* indicates the name of the streaming replication slot queried in :ref:`2 <drs_03_1131__li4276143622720>`.

#. Run the following statement to check whether the streaming replication slot is successfully deleted:

   .. code-block::

      select slot_name from pg_replication_slots where database = 'database';

   If the query result is empty, the streaming replication slot is deleted.

#. Repeat the preceding operations to ensure that the streaming replication slot on each primary DN is deleted.
