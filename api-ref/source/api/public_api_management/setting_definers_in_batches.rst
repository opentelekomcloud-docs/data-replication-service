:original_name: drs_03_0135.html

.. _drs_03_0135:

Setting Definers in Batches
===========================

Function
--------

The API is used to set whether to migrate Definers to the user in batches.

-  If you select **Yes**, the Definers of all source database objects will be migrated to the user. Other users do not have permissions on database objects unless they are authorized.
-  If you select **No**, the Definers of all source database objects will not be changed. You need to migrate all accounts and permissions of the source database in the next step.

Constraints
-----------

-  Only tasks that are being configured can call the API.

URI
---

POST /v3/{project_id}/jobs/batch-replace-definer

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

   +-----------+-----------+--------------------------------------------------------------------------------------+----------------------------------------------------------+
   | Parameter | Mandatory | Type                                                                                 | Description                                              |
   +===========+===========+======================================================================================+==========================================================+
   | jobs      | Yes       | Array of :ref:`ReplaceDefinerInfo <drs_03_0135__request_replacedefinerinfo>` objects | List of requests for setting replaceDefiners in batches. |
   +-----------+-----------+--------------------------------------------------------------------------------------+----------------------------------------------------------+

.. _drs_03_0135__request_replacedefinerinfo:

.. table:: **Table 4** ReplaceDefinerInfo

   +-----------------+-----------+---------+--------------------------------------------------------------------+
   | Parameter       | Mandatory | Type    | Description                                                        |
   +=================+===========+=========+====================================================================+
   | job_id          | Yes       | String  | Task ID.                                                           |
   +-----------------+-----------+---------+--------------------------------------------------------------------+
   | replace_definer | Yes       | Boolean | Whether to replace the definer with the destination database user. |
   +-----------------+-----------+---------+--------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 5** Response body parameters

   +-----------+-----------------------------------------------------------------------------+---------------------------------------------+
   | Parameter | Type                                                                        | Description                                 |
   +===========+=============================================================================+=============================================+
   | count     | Integer                                                                     | Total number.                               |
   +-----------+-----------------------------------------------------------------------------+---------------------------------------------+
   | results   | Array of :ref:`ModifyJobResp <drs_03_0135__response_modifyjobresp>` objects | List of tasks that are modified in batches. |
   +-----------+-----------------------------------------------------------------------------+---------------------------------------------+

.. _drs_03_0135__response_modifyjobresp:

.. table:: **Table 6** ModifyJobResp

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

Example of setting DR definers in batches:

.. code-block::

   https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-replace-definer

.. code-block::

   {
     "jobs" : [ {
       "job_id" : "7c685701-bfb5-4bb9-89f1-d0567f5jb502",
       "replace_definer" : true
     } ]
   }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "count" : 1,
     "results" : [ {
       "id" : "7c685701-bfb5-4bb9-89f1-d0567f5jb502",
       "status" : "success"
     } ]
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
