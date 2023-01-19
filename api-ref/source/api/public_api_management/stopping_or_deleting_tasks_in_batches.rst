:original_name: drs_03_0113.html

.. _drs_03_0113:

Stopping or Deleting Tasks in Batches
=====================================

Function
--------

This API is used to stop tasks in batches or delete real-time migration, real-time synchronization, and real-time DR tasks.

Constraints
-----------

-  Only tasks in the **CREATE_FAILED**, **RELEASE_RESOURCE_COMPLETE**, or **RELEASE_CHILD_TRANSFER_COMPLETE** state can be deleted. To delete a task in other states, stop the task first.
-  The parent task can call the API only in the dual-active DR scenario.

URI
---

DELETE /v3/{project_id}/jobs/batch-jobs

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

   +-----------+-----------+--------------------------------------------------------------------------+-------------------------------------------------------------+
   | Parameter | Mandatory | Type                                                                     | Description                                                 |
   +===========+===========+==========================================================================+=============================================================+
   | jobs      | Yes       | Array of :ref:`DeleteJobReq <drs_03_0113__request_deletejobreq>` objects | List of requests for stopping or deleting tasks in batches. |
   +-----------+-----------+--------------------------------------------------------------------------+-------------------------------------------------------------+

.. _drs_03_0113__request_deletejobreq:

.. table:: **Table 4** DeleteJobReq

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                                                             |
   +=================+=================+=================+=========================================================================================================================================================================================================================================================================+
   | delete_type     | Yes             | String          | The value can be **terminate**, **force_terminate**, or **delete**. **terminate** indicates that the migration task is stopped, **force_terminate** indicates that the migration task is forcibly stopped, and **delete** indicates that the migration task is deleted. |
   |                 |                 |                 |                                                                                                                                                                                                                                                                         |
   |                 |                 |                 | Values:                                                                                                                                                                                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                                                                                                         |
   |                 |                 |                 | -  **terminate**                                                                                                                                                                                                                                                        |
   |                 |                 |                 | -  **force_terminate**                                                                                                                                                                                                                                                  |
   |                 |                 |                 | -  **delete**                                                                                                                                                                                                                                                           |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_id          | Yes             | String          | Task ID.                                                                                                                                                                                                                                                                |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 202**

.. table:: **Table 5** Response body parameters

   +-----------+-----------------------------------------------------------------------------+--------------------------------------------------------------+
   | Parameter | Type                                                                        | Description                                                  |
   +===========+=============================================================================+==============================================================+
   | results   | Array of :ref:`DeleteJobResp <drs_03_0113__response_deletejobresp>` objects | Response body set for stopping or deleting tasks in batches. |
   +-----------+-----------------------------------------------------------------------------+--------------------------------------------------------------+
   | count     | Integer                                                                     | Total number.                                                |
   +-----------+-----------------------------------------------------------------------------+--------------------------------------------------------------+

.. _drs_03_0113__response_deletejobresp:

.. table:: **Table 6** DeleteJobResp

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

-  Request for stopping a task:

   .. code-block::

      https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-jobs

   .. code-block::

      {
        "jobs" : [ {
          "delete_type" : "terminate",
          "job_id" : "4c6ac8c0-2f51-426a-97b2-cb2c668jb201"
        }, {
          "delete_type" : "terminate",
          "job_id" : "6211d20d-0006-41da-836e-db3301ajb20b"
        } ]
      }

-  Request for deleting a task:

   .. code-block::

      https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-jobs

   .. code-block::

      {
        "jobs" : [ {
          "delete_type" : "delete",
          "job_id" : "140b5236-88ad-43c8-811c-1268453jb101"
        } ]
      }

Example Response
----------------

**Status code: 202**

Accepted

-  Example response for stopping a task

   .. code-block::

      {
        "count" : 2,
        "results" : [ {
          "id" : "4c6ac8c0-2f51-426a-97b2-cb2c668jb201",
          "status" : "success"
        }, {
          "id" : "6211d20d-0006-41da-836e-db3301ajb20b",
          "status" : "failed",
          "error_code" : "DRS.M01504",
          "error_msg" : "Another operation is being performed on the migration task or the migration task is abnormal. Try again later."
        } ]
      }

-  Example response for deleting a task

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
