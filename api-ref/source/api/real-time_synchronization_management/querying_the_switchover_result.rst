:original_name: drs_03_0148.html

.. _drs_03_0148:

Querying the Switchover Result
==============================

Function
--------

This API is used to query the dual-virtual IP address switchover result.

Constraints
-----------

Only synchronization between self-built databases supports querying the results of dual virtual IP address switchover.

URI
---

GET /v3/{project_id}/jobs/{job_id}/get-switch-vip-status

.. table:: **Table 1** Path parameters

   +------------+-----------+--------+---------------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                                 |
   +============+===========+========+=============================================================================================+
   | project_id | Yes       | String | Project ID of a tenant in a region                                                          |
   +------------+-----------+--------+---------------------------------------------------------------------------------------------+
   | job_id     | Yes       | String | Job ID of a tenant in a region. If the task is a cross-AZ task, the parent task ID is used. |
   +------------+-----------+--------+---------------------------------------------------------------------------------------------+

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

Response Parameters
-------------------

Status code: 200

.. table:: **Table 3** Response body parameters

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                       |
   +=======================+=======================+===================================================================================================+
   | id                    | String                | Task ID.                                                                                          |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | status                | String                | Status Values:                                                                                    |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **SWITCH_VIP_COMPLETE**: The switchover is successful.                                         |
   |                       |                       | -  **SWITCH_VIP_FAILED**: The switchover failed.                                                  |
   |                       |                       | -  **SWITCH_VIP_START**: The switchover is in progress.                                           |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code, which is optional and indicates the returned information about the failure status.    |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_msg             | String                | Error message, which is optional and indicates the returned information about the failure status. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+

Example Request
---------------

Example of batch primary/standby switchover:

.. code-block::

   https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/260e27fd-4976-44dc-9948-e1265e4jb201/get-switch-vip-status

Example Response
----------------

**Status code: 200**

Accepted

.. code-block::

   {
       "id": "260e27fd-4976-44dc-9948-e1265e4jb201",
       "status": "SWITCH_VIP_COMPLETE"
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
