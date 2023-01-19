:original_name: drs_03_0134.html

.. _drs_03_0134:

Changing the Passwords of the Sources and Destinations
======================================================

Function
--------

This API is used to change the passwords of the sources and destinations after a task is started.

Constraints
-----------

-  This API can be called only when the task is in the **STARTJOBING**, **STARTJOB_FAILED**, **FULL_TRANSFER_STARTED**, **FULL_TRANSFER_FAILED**, **FULL_TRANSFER_COMPLETE**, **INCRE_TRANSFER_STARTED**, **INCRE_TRANSFER_FAILED** or **PAUSING** state.
-  In the dual-active DR scenario, the parent task cannot call the API.

URI
---

PUT /v3/{project_id}/jobs/batch-modify-pwd

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

   +-----------+-----------+------------------------------------------------------------------------------------+------------------------------------------------------+
   | Parameter | Mandatory | Type                                                                               | Description                                          |
   +===========+===========+====================================================================================+======================================================+
   | jobs      | Yes       | Array of :ref:`ModifyPwdEndPoint <drs_03_0134__request_modifypwdendpoint>` objects | List of database passwords to be changed in batches. |
   +-----------+-----------+------------------------------------------------------------------------------------+------------------------------------------------------+

.. _drs_03_0134__request_modifypwdendpoint:

.. table:: **Table 4** ModifyPwdEndPoint

   +-----------------+-----------------+------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type                                                       | Description                                                                            |
   +=================+=================+============================================================+========================================================================================+
   | db_password     | Yes             | String                                                     | Database password.                                                                     |
   +-----------------+-----------------+------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | end_point_type  | Yes             | String                                                     | Type. **so** indicates the source database. **ta** indicates the destination database. |
   |                 |                 |                                                            |                                                                                        |
   |                 |                 |                                                            | Values:                                                                                |
   |                 |                 |                                                            |                                                                                        |
   |                 |                 |                                                            | -  **so**                                                                              |
   |                 |                 |                                                            | -  **ta**                                                                              |
   +-----------------+-----------------+------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | job_id          | Yes             | String                                                     | Task ID.                                                                               |
   +-----------------+-----------------+------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | kerberos        | No              | :ref:`KerberosVO <drs_03_0134__request_kerberosvo>` object | Information required for Kerberos authentication.                                      |
   +-----------------+-----------------+------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. _drs_03_0134__request_kerberosvo:

.. table:: **Table 5** KerberosVO

   ============== ========= ====== ========================
   Parameter      Mandatory Type   Description
   ============== ========= ====== ========================
   krb5_conf_file No        String krb5 configuration file.
   key_tab_file   No        String Key file.
   domain_name    No        String Domain name.
   user_principal No        String Kerberos user object.
   ============== ========= ====== ========================

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 6** Response body parameters

   +-----------+-----------------------------------------------------------------------------+---------------------------------------------+
   | Parameter | Type                                                                        | Description                                 |
   +===========+=============================================================================+=============================================+
   | count     | Integer                                                                     | Total number.                               |
   +-----------+-----------------------------------------------------------------------------+---------------------------------------------+
   | results   | Array of :ref:`ModifyJobResp <drs_03_0134__response_modifyjobresp>` objects | List of tasks that are modified in batches. |
   +-----------+-----------------------------------------------------------------------------+---------------------------------------------+

.. _drs_03_0134__response_modifyjobresp:

.. table:: **Table 7** ModifyJobResp

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
   | end_point_type        | String                | Type. **so** indicates the source database. **ta** indicates the destination database.            |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code, which is optional and indicates the returned information about the failure status.    |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_msg             | String                | Error message, which is optional and indicates the returned information about the failure status. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+

Example Request
---------------

Example request for changing the passwords of the sources and destinations:

.. code-block::

   https://{Endpoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-modify-pwd

.. code-block::

   {
     "jobs" : [ {
       "db_password" : "********",
       "end_point_type" : "so",
       "job_id" : "25df459d-a37c-41b9-bc2b-8c00ba32jb52"
     }, {
       "db_password" : "********",
       "end_point_type" : "ta",
       "job_id" : "25df459d-a37c-41b9-bc2b-8c00ba32jb52"
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
       "status" : "success",
       "end_point_type" : "so"
     }, {
       "id" : "8d0e8e36-a618-490d-8a46-8c61ac9jb502",
       "status" : "success",
       "end_point_type" : "ta"
     } ],
     "count" : 2
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
