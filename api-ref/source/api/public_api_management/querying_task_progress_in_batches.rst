:original_name: drs_03_0114.html

.. _drs_03_0114:

Querying Task Progress in Batches
=================================

Function
--------

This API is used to query the full progress and incremental delay information in batches based on the task ID.

URI
---

POST /v3/{project_id}/jobs/batch-progress

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

   +-----------+-----------+------------------+------------------------------------------------+
   | Parameter | Mandatory | Type             | Description                                    |
   +===========+===========+==================+================================================+
   | jobs      | Yes       | Array of strings | Request for querying task progress in batches. |
   +-----------+-----------+------------------+------------------------------------------------+

Response Parameters
-------------------

**Status code: 202**

.. table:: **Table 4** Response body parameters

   +-----------+-------------------------------------------------------------------------------------+---------------------------------------------------------------+
   | Parameter | Type                                                                                | Description                                                   |
   +===========+=====================================================================================+===============================================================+
   | count     | Integer                                                                             | Total number.                                                 |
   +-----------+-------------------------------------------------------------------------------------+---------------------------------------------------------------+
   | results   | Array of :ref:`QueryProgressResp <drs_03_0114__response_queryprogressresp>` objects | Response body for querying the migration progress in batches. |
   +-----------+-------------------------------------------------------------------------------------+---------------------------------------------------------------+

.. _drs_03_0114__response_queryprogressresp:

.. table:: **Table 5** QueryProgressResp

   +-----------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                      | Description                                                                                       |
   +=======================+===========================================================================+===================================================================================================+
   | job_id                | String                                                                    | Task ID.                                                                                          |
   +-----------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+
   | progress              | String                                                                    | Migration percentage.                                                                             |
   +-----------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+
   | incre_trans_delay     | String                                                                    | Incremental migration delay.                                                                      |
   +-----------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+
   | task_mode             | String                                                                    | Task mode. Values:                                                                                |
   |                       |                                                                           |                                                                                                   |
   |                       |                                                                           | -  **FULL_TRANS**: full migration                                                                 |
   |                       |                                                                           |                                                                                                   |
   |                       |                                                                           | -  **INCR_TRANS**: incremental migration                                                          |
   |                       |                                                                           |                                                                                                   |
   |                       |                                                                           | -  **FULL_INCR_TRANS**: full+incremental migration                                                |
   |                       |                                                                           |                                                                                                   |
   |                       |                                                                           |    In the single-active DR scenario, only **FULL_INCR_TRANS** is available.                       |
   +-----------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+
   | transfer_status       | String                                                                    | Task status.                                                                                      |
   +-----------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+
   | process_time          | String                                                                    | Migration time in timestamp format.                                                               |
   +-----------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+
   | remaining_time        | String                                                                    | Estimated remaining time.                                                                         |
   +-----------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+
   | progress_map          | Array of :ref:`ProgressInfo <drs_03_0114__response_progressinfo>` objects | Data, structure, and index migration progress information body.                                   |
   +-----------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+
   | error_code            | String                                                                    | Error code, which is optional and indicates the returned information about the failure status.    |
   +-----------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+
   | error_msg             | String                                                                    | Error message, which is optional and indicates the returned information about the failure status. |
   +-----------------------+---------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------+

.. _drs_03_0114__response_progressinfo:

.. table:: **Table 6** ProgressInfo

   ============== ====== =========================
   Parameter      Type   Description
   ============== ====== =========================
   completed      String Progress.
   remaining_time String Estimated remaining time.
   ============== ====== =========================

Example Request
---------------

Example of querying the DR progress:

.. code-block::

   https://{EndPoint}/drs/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-progress

.. code-block::

   {
     "jobs" : [ "8d0e8e36-a618-490d-8a46-8c61ac9jb502" ]
   }

Example Response
----------------

**Status code: 202**

OK

-  Example response 1 for querying the DR progress:

   .. code-block::

      {
        "count" : 1,
        "results" : [ {
          "progress" : "100",
          "job_id" : "8d0e8e36-a618-490d-8a46-8c61ac9jb502",
          "incre_trans_delay" : "0",
          "task_mode" : "FULL_INCR_TRANS",
          "transfer_status" : "INCRE_TRANSFER_STARTED",
          "process_time" : "1608274919000",
          "remaining_time" : "0"
        } ]
      }

-  Example response 2 for querying the DR progress:

   .. code-block::

      {
        "count" : 2,
        "results" : [ {
          "progress" : "100",
          "job_id" : "edae91cb-5892-49b6-a529-4921fb26jb21",
          "incre_trans_delay" : "0",
          "task_mode" : "FULL_INCR_TRANS",
          "transfer_status" : "INCRE_TRANSFER_STARTED",
          "process_time" : "1594864576000",
          "remaining_time" : "10"
        }, {
          "progress" : "0",
          "job_id" : "f95c5d83-d0c9-42bd-b295-38c31cd1jb15",
          "incre_trans_delay" : "-1",
          "task_mode" : "FULL_INCR_TRANS",
          "transfer_status" : "FULL_TRANSFER_COMPLETE",
          "process_time" : "0",
          "remaining_time" : "0",
          "progress_map" : {
            "struct" : {
              "completed" : "94%",
              "remaining_time" : null
            },
            "data" : {
              "completed" : "100%",
              "remaining_time" : null
            },
            "index" : {
              "completed" : "100%",
              "remaining_time" : null
            }
          }
        } ]
      }

Status Code
-----------

=========== ===========
Status Code Description
=========== ===========
202         Accepted
400         Bad Request
=========== ===========

Error Code
----------

For details, see :ref:`Error Code <drs_05_0004>`.
