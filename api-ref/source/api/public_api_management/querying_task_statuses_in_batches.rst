:original_name: drs_api_0150.html

.. _drs_api_0150:

Querying Task Statuses in Batches
=================================

Function
--------

This API is used to query task statuses in batches by task ID.

URI
---

POST /v3/{project_id}/jobs/batch-status

.. table:: **Table 1** Path parameters

   ========== ========= ====== ==================================
   Parameter  Mandatory Type   Description
   ========== ========= ====== ==================================
   project_id Yes       String Project ID of a tenant in a region
   ========== ========= ====== ==================================

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +-----------------+-----------------+-----------------+--------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                |
   +=================+=================+=================+============================================+
   | Content-Type    | Yes             | String          | The content type.                          |
   |                 |                 |                 |                                            |
   |                 |                 |                 | The default value is **application/json**. |
   +-----------------+-----------------+-----------------+--------------------------------------------+
   | X-Auth-Token    | Yes             | String          | User token obtained from IAM.              |
   +-----------------+-----------------+-----------------+--------------------------------------------+
   | X-Language      | No              | String          | Request language type                      |
   |                 |                 |                 |                                            |
   |                 |                 |                 | Default value: **en-us**                   |
   |                 |                 |                 |                                            |
   |                 |                 |                 | Values:                                    |
   |                 |                 |                 |                                            |
   |                 |                 |                 | -  **en-us**                               |
   |                 |                 |                 | -  **zh-cn**                               |
   +-----------------+-----------------+-----------------+--------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-----------+-----------+-------------------------------------------------------+----------------------------------+
   | Parameter | Mandatory | Type                                                  | Description                      |
   +===========+===========+=======================================================+==================================+
   | jobs      | Yes       | Array of strings                                      | Querying task details in batches |
   +-----------+-----------+-------------------------------------------------------+----------------------------------+
   | page_req  | No        | :ref:`PageReq <drs_api_0150__request_pagereq>` object | Pagination information.          |
   +-----------+-----------+-------------------------------------------------------+----------------------------------+

.. _drs_api_0150__request_pagereq:

.. table:: **Table 4** PageReq

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                          |
   +=================+=================+=================+======================================================================================================================================================+
   | cur_page        | No              | Integer         | Current page number, which cannot exceed the maximum number of pages. (Number of pages = Number of transferred job IDs/Number of tasks on each page) |
   |                 |                 |                 |                                                                                                                                                      |
   |                 |                 |                 | -  Minimum value: **1**.                                                                                                                             |
   |                 |                 |                 | -  Default value: **1**                                                                                                                              |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | per_page        | No              | Integer         | Number of items on each page. If this parameter is set to **0**, all items are obtained.                                                             |
   |                 |                 |                 |                                                                                                                                                      |
   |                 |                 |                 | -  Minimum value: **0**                                                                                                                              |
   |                 |                 |                 | -  Maximum value: **100**                                                                                                                            |
   |                 |                 |                 | -  Default value: **5**                                                                                                                              |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 5** Response body parameters

   +-----------+----------------------------------------------------------------------------------------+---------------------------+
   | Parameter | Type                                                                                   | Description               |
   +===========+========================================================================================+===========================+
   | results   | Array of :ref:`QueryJobStatusResp <drs_api_0150__response_queryjobstatusresp>` objects | Task status information   |
   +-----------+----------------------------------------------------------------------------------------+---------------------------+
   | count     | Integer                                                                                | Number of returned tasks. |
   +-----------+----------------------------------------------------------------------------------------+---------------------------+

.. _drs_api_0150__response_queryjobstatusresp:

.. table:: **Table 6** QueryJobStatusResp

   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                       |
   +=======================+=======================+===================================================================================================================+
   | id                    | String                | Task ID.                                                                                                          |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------+
   | status                | String                | Task status. Values:                                                                                              |
   |                       |                       |                                                                                                                   |
   |                       |                       | -  **CREATING**: The task is being created.                                                                       |
   |                       |                       | -  **CREATE_FAILED**: The task fails to be created.                                                               |
   |                       |                       | -  **CONFIGURATION**: The task is being configured.                                                               |
   |                       |                       | -  **STARTJOBING**: The task is being started.                                                                    |
   |                       |                       | -  **WAITING_FOR_START**: The task is waiting to be started.                                                      |
   |                       |                       | -  **START_JOB_FAILED**: The task fails to be started.                                                            |
   |                       |                       | -  **PAUSEING**: The task is being paused.                                                                        |
   |                       |                       | -  **FULL_TRANSFER_STARTED**: Full migration is in progress, and the DR scenario is initialized.                  |
   |                       |                       | -  **FULL_TRANSFER_FAILED**: Full migration failed. Initialization failed in the DR scenario.                     |
   |                       |                       | -  **FULL_TRANSFER_COMPLETE**: Full migration is complete, and the initialization is complete in the DR scenario. |
   |                       |                       | -  **INCRE_TRANSFER_STARTED**: Incremental migration is being performed, and the DR task is in progress.          |
   |                       |                       | -  **INCRE_TRANSFER_FAILED**: Incremental migration fails and a DR exception occurs.                              |
   |                       |                       | -  **RELEASE_RESOURCE_STARTED**: The task is being stopped.                                                       |
   |                       |                       | -  **RELEASE_RESOURCE_FAILED**: Stop task failed.                                                                 |
   |                       |                       | -  **RELEASE_RESOURCE_COMPLETE**: The task is stopped.                                                            |
   |                       |                       | -  **CHANGE_JOB_STARTED**: The task is being changed.                                                             |
   |                       |                       | -  **CHANGE_JOB_FAILED**: Change task failed.                                                                     |
   |                       |                       | -  **CHILD_TRANSFER_STARTING**: The subtask is being started.                                                     |
   |                       |                       | -  **CHILD_TRANSFER_STARTED**: The subtask is being migrated.                                                     |
   |                       |                       | -  **CHILD_TRANSFER_COMPLETE**: The subtask migration is complete.                                                |
   |                       |                       | -  **CHILD_TRANSFER_FAILED**: Migrate subtask failed.                                                             |
   |                       |                       | -  **RELEASE_CHILD_TRANSFER_STARTED**: The subtask is being stopped.                                              |
   |                       |                       | -  **RELEASE_CHILD_TRANSFER_COMPLETE**: The subtask is complete.                                                  |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code, which is optional and indicates the returned information about the failure status.                    |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------+
   | error_message         | String                | Error message, which is optional and indicates the returned information about the failure status.                 |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------+

Example Request
---------------

Example of querying task statuses in batches:

.. code-block::

   https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-status

.. code-block::

   {
     "jobs" : [ "9a470239-2308-4bb5-a6bc-1040402fjb21", "dc67695a-ee3e-49b8-a022-a099bd81jb21" ],
     "page_req" : {
       "cur_page" : 1,
       "per_page" : 10
     }
   }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "results" : [ {
       "id" : "9a470239-2308-4bb5-a6bc-1040402fjb21",
       "status" : "INCRE_TRANSFER_STARTED"
     }, {
       "id" : "dc67695a-ee3e-49b8-a022-a099bd81jb21",
       "status" : "INCRE_TRANSFER_FAILED"
     } ],
     "count" : 2
   }

Status Code
-----------

=========== ===========
Status Code Description
=========== ===========
200         OK
400         Bad Request
=========== ===========

Error Code
----------

For details, see :ref:`Error Code <drs_05_0004>`.
