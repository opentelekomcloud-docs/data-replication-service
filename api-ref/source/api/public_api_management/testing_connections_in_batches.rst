:original_name: drs_03_0105.html

.. _drs_03_0105:

Testing Connections in Batches
==============================

Function
--------

This API is used to test the connections to the source and destination ends in batches.

Constraints
-----------

-  After the task is created, you can test the connection only when the task status is **CONFIGURATION**.
-  In the dual-active DR scenario, the backward task can be executed only when the forward task is in **INCRE_TRANSFER_STARTED** state. The parent task cannot call the API.

URI
---

POST /v3/{project_id}/jobs/batch-connection

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

   +-----------+-----------+--------------------------------------------------------------------------+------------------------------------------------------+
   | Parameter | Mandatory | Type                                                                     | Description                                          |
   +===========+===========+==========================================================================+======================================================+
   | jobs      | Yes       | Array of :ref:`TestEndPoint <drs_03_0105__request_testendpoint>` objects | List of requests for testing connections in batches. |
   +-----------+-----------+--------------------------------------------------------------------------+------------------------------------------------------+

.. _drs_03_0105__request_testendpoint:

.. table:: **Table 4** TestEndPoint

   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter          | Mandatory       | Type            | Description                                                                                                                                                                                                               |
   +====================+=================+=================+===========================================================================================================================================================================================================================+
   | id                 | Yes             | String          | DRS task ID, which can be obtained from the task list or task details page.                                                                                                                                               |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | net_type           | Yes             | String          | Network type. Value:                                                                                                                                                                                                      |
   |                    |                 |                 |                                                                                                                                                                                                                           |
   |                    |                 |                 | -  **vpn**                                                                                                                                                                                                                |
   |                    |                 |                 | -  **vpc**                                                                                                                                                                                                                |
   |                    |                 |                 | -  **eip**                                                                                                                                                                                                                |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | db_type            | Yes             | String          | Database type. Value:                                                                                                                                                                                                     |
   |                    |                 |                 |                                                                                                                                                                                                                           |
   |                    |                 |                 | -  **mysql**                                                                                                                                                                                                              |
   |                    |                 |                 | -  **mongodb**                                                                                                                                                                                                            |
   |                    |                 |                 | -  **taurus**                                                                                                                                                                                                             |
   |                    |                 |                 | -  **postgresql**                                                                                                                                                                                                         |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ip                 | Yes             | String          | Database IP address.                                                                                                                                                                                                      |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | db_port            | No              | Integer         | Database port number. This parameter must be set to **0** for the MongoDB and DDS databases.                                                                                                                              |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | inst_id            | No              | String          | DB instance ID. This parameter is mandatory when the database is a cloud instance, for example, an RDS or GaussDB(for MySQL) instance.                                                                                    |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | db_user            | Yes             | String          | Database account.                                                                                                                                                                                                         |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | db_password        | Yes             | String          | Database password.                                                                                                                                                                                                        |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ssl_link           | No              | Boolean         | Whether SSL is enabled. If this parameter is set to **true**, you need to set parameters related to the SSL certificate.                                                                                                  |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ssl_cert_key       | No              | String          | SSL certificate content, which is a character string encrypted using BASE64 after the SSL certificate is obtained. This parameter is mandatory when **ssl_link** is set to **true**.                                      |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ssl_cert_name      | No              | String          | SSL certificate name. This parameter is mandatory when **ssl_link** is set to **true**.                                                                                                                                   |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ssl_cert_check_sum | No              | String          | The checksum value of the SSL certificate content encrypted using SHA256 after the SSL certificate is obtained, which is used for backend verification. This parameter is mandatory when **ssl_link** is set to **true**. |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ssl_cert_password  | No              | String          | The SSL certificate password. The certificate file name extension is .p12 and requires a password.                                                                                                                        |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | vpc_id             | No              | String          | ID of the VPC where the instance resides. This parameter is mandatory when the database is a cloud instance, for example, an RDS or GaussDB(for MySQL) instance.                                                          |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subnet_id          | No              | String          | ID of the subnet where the instance resides. This parameter is mandatory when the database is a cloud instance, for example, an RDS or GaussDB(for MySQL) instance.                                                       |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | end_point_type     | Yes             | String          | Source database: **so**. Destination database: **ta**.                                                                                                                                                                    |
   |                    |                 |                 |                                                                                                                                                                                                                           |
   |                    |                 |                 | Default value: **so**                                                                                                                                                                                                     |
   |                    |                 |                 |                                                                                                                                                                                                                           |
   |                    |                 |                 | Values:                                                                                                                                                                                                                   |
   |                    |                 |                 |                                                                                                                                                                                                                           |
   |                    |                 |                 | -  **so**                                                                                                                                                                                                                 |
   |                    |                 |                 | -  **ta**                                                                                                                                                                                                                 |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | region             | No              | String          | Region where the DB instance is located. This parameter is mandatory when the database is a cloud instance, for example, an RDS or GaussDB(for MySQL) instance.                                                           |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | project_id         | No              | String          | Project ID of the region where the user is located.                                                                                                                                                                       |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | db_name            | No              | String          | Database user name, which is the DDS authentication database.                                                                                                                                                             |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 5** Response body parameters

   +-----------+---------------------------------------------------------------------------+--------------------------------------------------+
   | Parameter | Type                                                                      | Description                                      |
   +===========+===========================================================================+==================================================+
   | results   | Array of :ref:`CheckJobResp <drs_03_0105__response_checkjobresp>` objects | Response body set for the batch test connection. |
   +-----------+---------------------------------------------------------------------------+--------------------------------------------------+
   | count     | Integer                                                                   | Total number of records.                         |
   +-----------+---------------------------------------------------------------------------+--------------------------------------------------+

.. _drs_03_0105__response_checkjobresp:

.. table:: **Table 6** CheckJobResp

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                       |
   +=======================+=======================+===================================================================================================+
   | id                    | String                | Task ID.                                                                                          |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | status                | String                | Test result. Value:                                                                               |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **success**: indicates that the connection test is successful.                                 |
   |                       |                       | -  **failed**: indicates that the connection test fails.                                          |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code, which is optional and indicates the returned information about the failure status.    |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_msg             | String                | Error message, which is optional and indicates the returned information about the failure status. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | success               | Boolean               | Whether the request is successful.                                                                |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+

Example Request
---------------

-  Example of a DDS real-time migration connection test:

   .. code-block::

      https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-connection

   .. code-block::

      {
        "jobs" : [ {
          "id" : "140b5236-88ad-43c8-811c-1268453jb101",
          "ip" : "192.168.4.66:8635,192.168.4.83:8635",
          "net_type" : "eip",
          "db_type" : "mongodb",
          "db_port" : 0,
          "db_user" : "root",
          "db_password" : "********",
          "inst_id" : "3cadd5a0ef724f55ac7fa5bcb5f4fc5fin02",
          "project_id" : "0549a6a31000d4e82fd1c00c3d6f2d76",
          "region" : "eu-de",
          "end_point_type" : "ta"
        } ]
      }

-  Example of an RDS MySQL real-time migration connection test:

   .. code-block::

      https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-connection

   .. code-block::

      {
        "jobs" : [ {
          "id" : "140b5236-88ad-43c8-811c-1268453jb101",
          "ip" : "192.168.0.131",
          "net_type" : "eip",
          "db_type" : "mysql",
          "db_port" : 3306,
          "db_user" : "root",
          "db_password" : "********",
          "inst_id" : "e05a3679efe241d8b5dee80b17c1a863in01",
          "project_id" : "054ba152d480d55b2f5dc0069e7ddef0",
          "region" : "eu-de",
          "end_point_type" : "ta"
        } ]
      }

-  Example of a real-time MySQL migration connection test:

   .. code-block::

      https://{Endpoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-connection

   .. code-block::

      {
        "jobs" : [ {
          "id" : "140b5236-88ad-43c8-811c-1268453jb101",
          "ip" : "192.168.0.27",
          "net_type" : "eip",
          "db_type" : "mysql",
          "db_port" : 3306,
          "db_user" : "root",
          "db_password" : "********",
          "ssl_link" : false,
          "end_point_type" : "so"
        } ]
      }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "results" : [ {
       "success" : true,
       "id" : "140b5236-88ad-43c8-811c-1268453jb101",
       "status" : "success"
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
