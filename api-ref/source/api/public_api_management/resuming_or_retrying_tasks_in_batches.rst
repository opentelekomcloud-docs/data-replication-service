:original_name: drs_03_0132.html

.. _drs_03_0132:

Resuming or Retrying Tasks in Batches
=====================================

Function
--------

-  This API is used to retry failed tasks.
-  In the dual-active DR scenario, the parent task cannot call the API.

URI
---

POST /v3/{project_id}/jobs/batch-retry-task

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

   +-----------+-----------+--------------------------------------------------------------------+--------------------------------------------------------+
   | Parameter | Mandatory | Type                                                               | Description                                            |
   +===========+===========+====================================================================+========================================================+
   | jobs      | Yes       | Array of :ref:`RetryInfo <drs_03_0132__request_retryinfo>` objects | List of requests for resuming upload tasks in batches. |
   +-----------+-----------+--------------------------------------------------------------------+--------------------------------------------------------+

.. _drs_03_0132__request_retryinfo:

.. table:: **Table 4** RetryInfo

   +-----------------+-----------+---------+--------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory | Type    | Description                                                                                |
   +=================+===========+=========+============================================================================================+
   | job_id          | Yes       | String  | Task ID.                                                                                   |
   +-----------------+-----------+---------+--------------------------------------------------------------------------------------------+
   | is_sync_re_edit | No        | Boolean | This parameter is mandatory when a task is resumed or retried and must be set to **true**. |
   +-----------------+-----------+---------+--------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 5** Response body parameters

   +-----------+-----------------------------------------------------------------------------+-----------------------------------------------+
   | Parameter | Type                                                                        | Description                                   |
   +===========+=============================================================================+===============================================+
   | results   | Array of :ref:`RetryTaskResp <drs_03_0132__response_retrytaskresp>` objects | List of tasks that can be resumed in batches. |
   +-----------+-----------------------------------------------------------------------------+-----------------------------------------------+
   | count     | Integer                                                                     | Total number.                                 |
   +-----------+-----------------------------------------------------------------------------+-----------------------------------------------+

.. _drs_03_0132__response_retrytaskresp:

.. table:: **Table 6** RetryTaskResp

   +------------+--------+---------------------------------------------------------------------------------------------------+
   | Parameter  | Type   | Description                                                                                       |
   +============+========+===================================================================================================+
   | id         | String | Task ID.                                                                                          |
   +------------+--------+---------------------------------------------------------------------------------------------------+
   | status     | String | Status                                                                                            |
   +------------+--------+---------------------------------------------------------------------------------------------------+
   | error_code | String | Error code, which is optional and indicates the returned information about the failure status.    |
   +------------+--------+---------------------------------------------------------------------------------------------------+
   | error_msg  | String | Error message, which is optional and indicates the returned information about the failure status. |
   +------------+--------+---------------------------------------------------------------------------------------------------+

Example Request
---------------

Example of resuming tasks in batches:

.. code-block::

   https://{Endpoint}/v3/054babbbde80d4602f5cc0043a40ed8c/jobs/batch-retry-task

.. code-block::

   {
     "jobs" : [ {
       "job_id" : "140b5236-88ad-43c8-811c-1268453jb101"
     } ]
   }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "results" : [ {
       "id" : "140b5236-88ad-43c8-811c-1268453jb101",
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
