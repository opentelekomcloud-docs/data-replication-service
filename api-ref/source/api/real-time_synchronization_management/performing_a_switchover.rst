:original_name: drs_03_0147.html

.. _drs_03_0147:

Performing a Switchover
=======================

Function
--------

This API is used to switch over virtual IP addresses.

Constraints
-----------

Only synchronization between self-built databases supports the dual virtual IP address switchover.

URI
---

POST /v3/{project_id}/jobs/{job_id}/switch-vip

.. table:: **Table 1** Path parameters

   +------------+-----------+--------+---------------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                                 |
   +============+===========+========+=============================================================================================+
   | project_id | Yes       | String | Project ID of a tenant in a region.                                                         |
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

.. table:: **Table 3** Request body parameters

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                    |
   +=================+=================+=================+================================================================================+
   | mode            | Yes             | String          | Switchover type. Values:                                                       |
   |                 |                 |                 |                                                                                |
   |                 |                 |                 | -  **source**: Switch over the virtual IP address of the source database.      |
   |                 |                 |                 | -  **target**: Switch over the virtual IP address of the destination database. |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 202**

.. table:: **Table 4** Response body parameters

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                       |
   +=======================+=======================+===================================================================================================+
   | id                    | String                | Task ID.                                                                                          |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | status                | String                | Status Values:                                                                                    |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **success**: The task is successful.                                                           |
   |                       |                       | -  **failed**: The task fails.                                                                    |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code, which is optional and indicates the returned information about the failure status.    |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_msg             | String                | Error message, which is optional and indicates the returned information about the failure status. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+

Example Request
---------------

Example of batch primary/standby switchover:

.. code-block::

   https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/8c81a12f-2581-4424-a3ab-70ed874jb201/switch-vip

.. code-block::

   {
       "mode": "source"
   }

Example Response
----------------

**Status code: 202**

Accepted

.. code-block::

   {
       "id": "8c81a12f-2581-4424-a3ab-70ed874jb201",
       "status": "success"
   }

Status Code
-----------

=========== ===========
Status Code Description
=========== ===========
202         Accepted
400         Bad Request
=========== ===========

Error code
----------

For details, see :ref:`Error Code <drs_05_0004>`.
