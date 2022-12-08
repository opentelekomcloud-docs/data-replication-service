:original_name: drs_15_0021.html

.. _drs_15_0021:

Checking Whether the Source Database Contains Triggers or Events
================================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the source database contains triggers or events

   +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                                   | Whether the source database contains triggers or events                                                                                                                                                                                                                                                           |
   +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                                  | To prevent unexpected operations on the destination database automatically triggered by triggers or events, this task starts the trigger or event migration only after you stop the task. If you close or disconnect the source database connection during the task running, triggers or events are not migrated. |
   +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item to Be Confirmed and Handling Suggestion | Item to be confirmed: The source database contains triggers or events.                                                                                                                                                                                                                                            |
   |                                              |                                                                                                                                                                                                                                                                                                                   |
   |                                              | Handling suggestion: Stop the task first and then disconnect the network to ensure the completeness of the migration.                                                                                                                                                                                             |
   +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
