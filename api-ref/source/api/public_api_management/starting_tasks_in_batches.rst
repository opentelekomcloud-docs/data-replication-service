:original_name: drs_03_0112.html

.. _drs_03_0112:

Starting Tasks in Batches
=========================

Function
--------

This API is used to start real-time migration, synchronization, and disaster recovery tasks in batches.

Constraints
-----------

-  This API can be called only after all tasks are configured.
-  In the dual-active DR scenario, this operation can be performed only when the forward task status is **INCRE_TRANSFER_STARTED** and **RPO&RTO** is less than 60s. For backward tasks, this operation can be performed only after all tasks are configured. The parent task does not support this operation.

URI
---

POST /v3/{project_id}/jobs/batch-starting

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

   +-----------+-----------+--------------------------------------------------------------------+---------------------------------------------+
   | Parameter | Mandatory | Type                                                               | Description                                 |
   +===========+===========+====================================================================+=============================================+
   | jobs      | Yes       | Array of :ref:`StartInfo <drs_03_0112__request_startinfo>` objects | Request list for starting tasks in batches. |
   +-----------+-----------+--------------------------------------------------------------------+---------------------------------------------+

.. _drs_03_0112__request_startinfo:

.. table:: **Table 4** StartInfo

   +------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                                                                                     |
   +============+===========+========+=================================================================================================================================================+
   | job_id     | Yes       | String | Task ID.                                                                                                                                        |
   +------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | start_time | No        | String | Task start time. The timestamp is accurate to milliseconds, for example, 1608188903063. If the value is empty, the task is started immediately. |
   +------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 202**

.. table:: **Table 5** Response body parameters

   +-----------+---------------------------------------------------------------------------+------------------------------------------------------------------------+
   | Parameter | Type                                                                      | Description                                                            |
   +===========+===========================================================================+========================================================================+
   | results   | Array of :ref:`StartJobResp <drs_03_0112__response_startjobresp>` objects | List of real-time disaster recovery tasks that are started in batches. |
   +-----------+---------------------------------------------------------------------------+------------------------------------------------------------------------+
   | count     | Integer                                                                   | Total number.                                                          |
   +-----------+---------------------------------------------------------------------------+------------------------------------------------------------------------+

.. _drs_03_0112__response_startjobresp:

.. table:: **Table 6** StartJobResp

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                       |
   +=======================+=======================+===================================================================================================+
   | id                    | String                | Task ID.                                                                                          |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | status                | String                | Status Values:                                                                                    |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **success**                                                                                    |
   |                       |                       | -  **failed**                                                                                     |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code, which is optional and indicates the returned information about the failure status.    |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_msg             | String                | Error message, which is optional and indicates the returned information about the failure status. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+

Example Request
---------------

Example of starting real-time DR tasks in batches:

.. code-block::

   https://{Endpoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-starting

.. code-block::

   {
     "jobs" : [ {
       "job_id" : "140b5236-88ad-43c8-811c-1268453jb101"
     } ]
   }

Example Response
----------------

**Status code: 202**

Accepted

.. code-block::

   {
     "count" : 1,
     "results" : [ {
       "id" : "140b5236-88ad-43c8-811c-1268453jb101",
       "status" : "success"
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
