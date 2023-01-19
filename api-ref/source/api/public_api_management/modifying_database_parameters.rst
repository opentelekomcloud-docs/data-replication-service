:original_name: drs_03_0131.html

.. _drs_03_0131:

Modifying Database Parameters
=============================

Function
--------

This API is to modify database parameters.

Constraints
-----------

You need to call the API for obtaining database parameters for MySQL migration and MySQL DR tasks. This API can be called only when **job_direction** is set to **up** and the task status is **CONFIGURATION**. In dual-active DR mode, the parent task does not support this operation.

URI
---

POST /v3/{project_id}/jobs/{job_id}/params

.. table:: **Table 1** Path parameters

   ========== ========= ====== ==================================
   Parameter  Mandatory Type   Description
   ========== ========= ====== ==================================
   job_id     Yes       String Task ID.
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

   +-----------------+-----------------+----------------------------------------------------------------------------+--------------------------------------------------+
   | Parameter       | Mandatory       | Type                                                                       | Description                                      |
   +=================+=================+============================================================================+==================================================+
   | group           | Yes             | String                                                                     | Parameter Groups Values:                         |
   |                 |                 |                                                                            |                                                  |
   |                 |                 |                                                                            | -  **common**                                    |
   |                 |                 |                                                                            | -  **performance**                               |
   +-----------------+-----------------+----------------------------------------------------------------------------+--------------------------------------------------+
   | params          | Yes             | Array of :ref:`ParamsReqBean <drs_03_0131__request_paramsreqbean>` objects | Information about the parameters to be modified. |
   +-----------------+-----------------+----------------------------------------------------------------------------+--------------------------------------------------+

.. _drs_03_0131__request_paramsreqbean:

.. table:: **Table 4** ParamsReqBean

   +--------------+-----------+--------+----------------------------------------------+
   | Parameter    | Mandatory | Type   | Description                                  |
   +==============+===========+========+==============================================+
   | key          | Yes       | String | Database parameter name.                     |
   +--------------+-----------+--------+----------------------------------------------+
   | target_value | Yes       | String | Parameter value of the destination database. |
   +--------------+-----------+--------+----------------------------------------------+

Response Parameters
-------------------

**Status code: 202**

.. table:: **Table 5** Response body parameters

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                       |
   +=======================+=======================+===================================================================================================+
   | success               | Boolean               | Whether the parameters are modified.                                                              |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | should_restart        | String                | Whether the instance needs to be restarted. Values:                                               |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **true**                                                                                       |
   |                       |                       | -  **false**                                                                                      |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code, which is optional and indicates the returned information about the failure status.    |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_msg             | String                | Error message, which is optional and indicates the returned information about the failure status. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+

Example Request
---------------

Example of modifying database parameters:

.. code-block::

   https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/140b5236-88ad-43c8-811c-1268453jb101/params

.. code-block::

   {
     "group" : "performance",
     "params" : [ {
       "key" : "binlog_stmt_cache_size",
       "target_value" : "32678"
     }, {
       "key" : "bulk_insert_buffer_size",
       "target_value" : "8388608"
     } ]
   }

Example Response
----------------

**Status code: 202**

Accepted

.. code-block::

   {
     "success" : true,
     "should_restart" : "false"
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
