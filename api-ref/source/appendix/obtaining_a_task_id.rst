:original_name: drs_api_0115.html

.. _drs_api_0115:

Obtaining a Task ID
===================

A task ID is required for some URLs when an API is called. This section describes how to obtain a task ID.

Obtaining a Task ID from the Console
------------------------------------

#. You have logged in to the DRS management console.

#. In the task list, view the task ID.

   Alternatively, click the task name and view the task ID on the **Basic Information** tab.

Obtaining a Task ID Through an API
----------------------------------

You can also obtain the task ID by calling the API in :ref:`Creating Tasks in Batches <drs_03_0104>`.

The following is an example response after a task is successfully created. In the response, **id** indicates the task ID.

.. code-block::

   {
     "results" : [ {
       "id" : "e11eaf8f-71ef-4fad-8890-aed7572ajb11",
       "name" : "DRS-9228",
       "status" : "CREATING",
       "create_time" : "1599188556112"
     } ],
     "count" : 1
   }
