:original_name: drs_03_0133.html

.. _drs_03_0133:

Pausing Tasks in Batches
========================

Function
--------

This API is used to pause tasks in batches.

Constraints
-----------

-  Migration and synchronization tasks can be paused.
-  Only tasks in the FULL_TRANSFER_STARTED, FULL_TRANSFER_FAILED, FULL_TRANSFER_COMPLETE, INCRE_TRANSFER_STARTED or INCRE_TRANSFER_FAILED state can be paused.

URI
---

POST /v3/{project_id}/jobs/batch-pause-task

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

   +-----------+-----------+--------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type                                                               | Description                                                                                     |
   +===========+===========+====================================================================+=================================================================================================+
   | jobs      | Yes       | Array of :ref:`PauseInfo <drs_03_0133__request_pauseinfo>` objects | The value cannot contain empty objects. The value of **job_id** must comply with the UUID rule. |
   +-----------+-----------+--------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+

.. _drs_03_0133__request_pauseinfo:

.. table:: **Table 4** PauseInfo

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | job_id          | Yes             | String          | Task ID.                                                                     |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | pause_mode      | Yes             | String          | Pause type. **target**: Stop replay. **all**: Stop log capturing and replay. |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | Values:                                                                      |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | -  **target**                                                                |
   |                 |                 |                 | -  **all**                                                                   |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 5** Response body parameters

   +-----------+---------------------------------------------------------------------------+-------------------------------------------+
   | Parameter | Type                                                                      | Description                               |
   +===========+===========================================================================+===========================================+
   | results   | Array of :ref:`PauseJobResp <drs_03_0133__response_pausejobresp>` objects | List of tasks to be suspended in batches. |
   +-----------+---------------------------------------------------------------------------+-------------------------------------------+
   | count     | Integer                                                                   | Total number.                             |
   +-----------+---------------------------------------------------------------------------+-------------------------------------------+

.. _drs_03_0133__response_pausejobresp:

.. table:: **Table 6** PauseJobResp

   +------------+--------+---------------------------------------------------------------------------------------------------+
   | Parameter  | Type   | Description                                                                                       |
   +============+========+===================================================================================================+
   | id         | String | Task ID.                                                                                          |
   +------------+--------+---------------------------------------------------------------------------------------------------+
   | status     | String | Pause result.                                                                                     |
   +------------+--------+---------------------------------------------------------------------------------------------------+
   | error_code | String | Error code, which is optional and indicates the returned information about the failure status.    |
   +------------+--------+---------------------------------------------------------------------------------------------------+
   | error_msg  | String | Error message, which is optional and indicates the returned information about the failure status. |
   +------------+--------+---------------------------------------------------------------------------------------------------+

Example Request
---------------

Example of suspending tasks in batches:

.. code-block::

   https://{Endpoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-pause-task

.. code-block::

   {
     "jobs" : [ {
       "job_id" : "8d0e8e36-a618-490d-8a46-8c61ac9jb502",
       "pause_mode" : "target"
     } ]
   }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "results" : [ {
       "id" : "8d0e8e36-a618-490d-8a46-8c61ac9jb502",
       "status" : "success"
     } ],
     "count" : 1
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
