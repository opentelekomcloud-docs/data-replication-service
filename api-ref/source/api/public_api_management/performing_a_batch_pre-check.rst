:original_name: drs_03_0110.html

.. _drs_03_0110:

Performing a Batch Pre-Check
============================

Function
--------

This API is used to perform batch pre-check to check whether the migration, synchronization, DR can be performed.

Constraints
-----------

-  After a task is created, the task status is **CONFIGURATION**. The task can be invoked only after the test of connections to the source and destination databases is successful and the API for modifying the task is invoked.
-  In the dual-active DR scenario, when the forward task status is **INCRE_TRANSFER_STARTED**, the backward task does not need to call this API, and the parent task cannot call this API.

URI
---

POST /v3/{project_id}/jobs/batch-precheck

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

   +-----------+-----------+--------------------------------------------------------------------------+---------------------------------------+
   | Parameter | Mandatory | Type                                                                     | Description                           |
   +===========+===========+==========================================================================+=======================================+
   | jobs      | Yes       | Array of :ref:`PreCheckInfo <drs_03_0110__request_precheckinfo>` objects | The list of batch pre-check requests. |
   +-----------+-----------+--------------------------------------------------------------------------+---------------------------------------+

.. _drs_03_0110__request_precheckinfo:

.. table:: **Table 4** PreCheckInfo

   +-----------------+-----------------+-----------------+------------------------+
   | Parameter       | Mandatory       | Type            | Description            |
   +=================+=================+=================+========================+
   | job_id          | Yes             | String          | Task ID.               |
   +-----------------+-----------------+-----------------+------------------------+
   | precheck_mode   | Yes             | String          | Pre-check mode. Value: |
   |                 |                 |                 |                        |
   |                 |                 |                 | -  **forStartJob**     |
   +-----------------+-----------------+-----------------+------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 5** Response body parameters

   +-----------+-----------------------------------------------------------------------------------+--------------------------+
   | Parameter | Type                                                                              | Description              |
   +===========+===================================================================================+==========================+
   | results   | Array of :ref:`PostPreCheckResp <drs_03_0110__response_postprecheckresp>` objects | Pre-check response body. |
   +-----------+-----------------------------------------------------------------------------------+--------------------------+
   | count     | Integer                                                                           | Total number.            |
   +-----------+-----------------------------------------------------------------------------------+--------------------------+

.. _drs_03_0110__response_postprecheckresp:

.. table:: **Table 6** PostPreCheckResp

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                       |
   +=======================+=======================+===================================================================================================+
   | id                    | String                | Task ID.                                                                                          |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | precheck_id           | String                | Pre-check ID.                                                                                     |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | status                | String                | Success or failure status. Values:                                                                |
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

Example of MySQL pre-check for real-time migration:

.. code-block::

   https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-precheck

.. code-block::

   {
     "jobs" : [ {
       "job_id" : "140b5236-88ad-43c8-811c-1268453jb101",
       "precheck_mode" : "forStartJob"
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
       "status" : "success",
       "precheck_id" : "140b5236-88ad-43c8-811c-1268453jb101"
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
