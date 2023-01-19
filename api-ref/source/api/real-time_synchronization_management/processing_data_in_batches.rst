:original_name: drs_api_0103.html

.. _drs_api_0103:

Processing Data in Batches
==========================

Function
--------

This API is used to add rules for data processing.

Constraints
-----------

-  Each table has only one verification rule.
-  MySQL source database supports a maximum of 10,000 tables at a time.
-  The filter criteria do not support the package, function, variable, and constant that are unique to a certain database engine. You must use standardized SQL.

URI
---

POST /v3/{project_id}/jobs/batch-transformation

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

   +-----------+-----------+-------------------------------------------------------------------------------------------------------+-------------------------------------------------------+
   | Parameter | Mandatory | Type                                                                                                  | Description                                           |
   +===========+===========+=======================================================================================================+=======================================================+
   | jobs      | Yes       | Array of :ref:`CheckDataTransformationReq <drs_api_0103__request_checkdatatransformationreq>` objects | Requests for adding data processing rules in batches. |
   +-----------+-----------+-------------------------------------------------------------------------------------------------------+-------------------------------------------------------+

.. _drs_api_0103__request_checkdatatransformationreq:

.. table:: **Table 4** CheckDataTransformationReq

   +-----------------------+-----------------+-------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory       | Type                                                                                | Description                                                                                                                                                                                                                                |
   +=======================+=================+=====================================================================================+============================================================================================================================================================================================================================================+
   | job_id                | No              | String                                                                              | Task ID.                                                                                                                                                                                                                                   |
   +-----------------------+-----------------+-------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | object_info           | No              | Array of :ref:`DatabaseObjectVO <drs_api_0103__request_databaseobjectvo>` objects   | Object information. This parameter is mandatory when a processing rule is generated.                                                                                                                                                       |
   +-----------------------+-----------------+-------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | transformation_info   | Yes             | :ref:`TransformationInfo <drs_api_0103__request_transformationinfo>` object         | Processing information.                                                                                                                                                                                                                    |
   +-----------------------+-----------------+-------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | config_transformation | No              | :ref:`ConfigTransformationVo <drs_api_0103__request_configtransformationvo>` object | -  Configuration information. If there are multiple associated tables, generate multiple configuration rules. The data that meets the configuration conditions is temporarily stored in the cache and used in the data filtering scenario. |
   |                       |                 |                                                                                     | -  The database name and table name can contain digits, letters, and underscores (_).                                                                                                                                                      |
   |                       |                 |                                                                                     | -  Ensure that the column names, primary keys, and indexes are the same as those in the source database.                                                                                                                                   |
   +-----------------------+-----------------+-------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _drs_api_0103__request_databaseobjectvo:

.. table:: **Table 5** DatabaseObjectVO

   +-----------+-----------+--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type   | Description                                                                                                                                                            |
   +===========+===========+========+========================================================================================================================================================================+
   | id        | No        | String | Database name and database table name. For example, the format is **lxl_test1-*-*-test_1**, where **lxl_test1** is the database name and **test_1** is the table name. |
   +-----------+-----------+--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | select    | No        | String | Whether to select advanced configuration. The value is **true**.                                                                                                       |
   +-----------+-----------+--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | leavesNum | No        | String | Level of a processing object. The default value is **0**.                                                                                                              |
   +-----------+-----------+--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _drs_api_0103__request_transformationinfo:

.. table:: **Table 6** TransformationInfo

   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter           | Mandatory       | Type            | Description                                                                                                                                                    |
   +=====================+=================+=================+================================================================================================================================================================+
   | transformation_type | Yes             | String          | -  The processing rule value is **contentConditionalFilter**.                                                                                                  |
   |                     |                 |                 |                                                                                                                                                                |
   |                     |                 |                 | -  The configuration rule value is **configConditionalFilter**.                                                                                                |
   |                     |                 |                 |                                                                                                                                                                |
   |                     |                 |                 |    Values:                                                                                                                                                     |
   |                     |                 |                 |                                                                                                                                                                |
   |                     |                 |                 |    -  **contentConditionalFilter**                                                                                                                             |
   |                     |                 |                 |    -  **configConditionalFilter**                                                                                                                              |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | value               | Yes             | String          | Filter criteria. The processing rule value is a SQL statement, and the configuration rule value is **config**. The value contains a maximum of 256 characters. |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _drs_api_0103__request_configtransformationvo:

.. table:: **Table 7** ConfigTransformationVo

   +-------------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter         | Mandatory | Type   | Description                                                                                                                               |
   +===================+===========+========+===========================================================================================================================================+
   | db_table_name     | Yes       | String | *Database-name.Table-name*, for example, **lxl_test1.test_1**, where **lxl_test1** is the database name and **test_1** is the table name. |
   +-------------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | db_name           | Yes       | String | Database name. The value contains a maximum of 256 characters.                                                                            |
   +-------------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | table_name        | Yes       | String | Table name The value contains a maximum of 256 characters.                                                                                |
   +-------------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | col_names         | Yes       | String | Column name The value contains a maximum of 256 characters.                                                                               |
   +-------------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | prim_key_or_index | Yes       | String | Primary key or unique index The value contains a maximum of 256 characters.                                                               |
   +-------------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | indexs            | Yes       | String | Index that requires optimization. The value contains a maximum of 256 characters.                                                         |
   +-------------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | values            | Yes       | String | Filtering criteria. The value contains a maximum of 256 characters.                                                                       |
   +-------------------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 8** Response body parameters

   +-----------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | Parameter | Type                                                                                           | Description                          |
   +===========+================================================================================================+======================================+
   | results   | Array of :ref:`DataTransformationResp <drs_api_0103__response_datatransformationresp>` objects | Batch data processing response list. |
   +-----------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | count     | String                                                                                         | Total number.                        |
   +-----------+------------------------------------------------------------------------------------------------+--------------------------------------+

.. _drs_api_0103__response_datatransformationresp:

.. table:: **Table 9** DataTransformationResp

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

-  Example of MySQL data generation configuration rules:

   .. code-block::

      https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-transformation

   .. code-block::

      {
        "jobs" : [ {
          "job_id" : "e894593d-5e0a-4652-af7e-1b0c239jb201",
          "object_info" : [ ],
          "transformation_info" : {
            "transformation_type" : "configConditionalFilter",
            "value" : "config"
          },
          "config_transformation" : {
            "col_names" : "id,name",
            "db_name" : "lxl_test1",
            "db_table_name" : "lxl_test1.test_1",
            "indexs" : "name",
            "prim_key_or_index" : "id",
            "table_name" : "test_1",
            "values" : "name like '%a%'"
          }
        } ]
      }

-  Example of MySQL data generation and processing rules:

   .. code-block::

      https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-transformation

   .. code-block::

      {
        "jobs" : [ {
          "job_id" : "e894593d-5e0a-4652-af7e-1b0c239jb201",
          "object_info" : [ {
            "id" : "lxl_test1-*-*-test_1",
            "select" : "true"
          } ],
          "transformation_info" : {
            "transformation_type" : "contentConditionalFilter",
            "value" : "id>5"
          }
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
       "id" : "e894593d-5e0a-4652-af7e-1b0c239jb201",
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
