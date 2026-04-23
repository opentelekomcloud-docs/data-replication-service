:original_name: drs_03_0239.html

.. _drs_03_0239:

Querying Available Node Specifications
======================================

Function
--------

This API is used to query available node specifications.

URI
---

GET /v3/{project_id}/node-type

.. table:: **Table 1** Path parameters

   +-----------------+-----------------+-----------------+----------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                    |
   +=================+=================+=================+================================================================+
   | project_id      | Yes             | String          | Project ID of a tenant in a region.                            |
   |                 |                 |                 |                                                                |
   |                 |                 |                 | For details, see :ref:`Obtaining a Project ID <drs_api_0106>`. |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------+

.. table:: **Table 2** Query parameters

   +---------------------+-----------------+-----------------+------------------------------------------------------------------+
   | Parameter           | Mandatory       | Type            | Description                                                      |
   +=====================+=================+=================+==================================================================+
   | engine_type         | Yes             | String          | Engine type of a DRS task.                                       |
   |                     |                 |                 |                                                                  |
   |                     |                 |                 | Values:                                                          |
   |                     |                 |                 |                                                                  |
   |                     |                 |                 | -  **mysql**: migration and synchronization from MySQL to MySQL  |
   |                     |                 |                 | -  **mongodb**: migration from MongoDB to DDS                    |
   |                     |                 |                 | -  **cloudDataGuard-mysql**: DR from MySQL to MySQL              |
   |                     |                 |                 | -  **mysql-to-taurus**: synchronization from MySQL to TaurusDB   |
   |                     |                 |                 | -  **postgresql**: synchronization from PostgreSQL to PostgreSQL |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------+
   | db_use_type         | Yes             | String          | Migration scenario.                                              |
   |                     |                 |                 |                                                                  |
   |                     |                 |                 | Values:                                                          |
   |                     |                 |                 |                                                                  |
   |                     |                 |                 | -  **migration**: real-time migration                            |
   |                     |                 |                 | -  **sync**: real-time synchronization                           |
   |                     |                 |                 | -  **cloudDataGuard**: real-time disaster recovery               |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------+
   | job_direction       | Yes             | String          | Migration direction.                                             |
   |                     |                 |                 |                                                                  |
   |                     |                 |                 | Values:                                                          |
   |                     |                 |                 |                                                                  |
   |                     |                 |                 | -  **up**: to the cloud                                          |
   |                     |                 |                 | -  **down**: out of the cloud                                    |
   |                     |                 |                 | -  **non-dbs**: self-built databases                             |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------+
   | is_use_sellout_info | No              | Boolean         | Whether to check if resources are sold out.                      |
   |                     |                 |                 |                                                                  |
   |                     |                 |                 | Default value: **false**                                         |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------+
   | is_multi_write      | No              | Boolean         | Whether dual-active disaster recovery is used.                   |
   |                     |                 |                 |                                                                  |
   |                     |                 |                 | Default value: **false**                                         |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 3** Request header parameters

   +-----------------+-----------------+-----------------+--------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                |
   +=================+=================+=================+============================================+
   | Content-Type    | No              | String          | The content type.                          |
   |                 |                 |                 |                                            |
   |                 |                 |                 | The default value is **application/json**. |
   +-----------------+-----------------+-----------------+--------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                    |
   +=======================+=======================+================================================================================================================+
   | node_types            | Array of objects      | Node specification list.                                                                                       |
   |                       |                       |                                                                                                                |
   |                       |                       | For details, see :ref:`Table 5 <drs_03_0239__en-us_topic_0000001822352738_response_querysupportnodetypebean>`. |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------+

.. _drs_03_0239__en-us_topic_0000001822352738_response_querysupportnodetypebean:

.. table:: **Table 5** Data structure description of field **node_types**

   ========== ======= ====================================
   Parameter  Type    Description
   ========== ======= ====================================
   node_type  String  Specifications.
   is_sellout Boolean Whether specifications are sold out.
   ========== ======= ====================================

Example Request
---------------

Querying available node specifications

.. code-block::

   https://{endpoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/node_type?db_use_type=sync&engine_type=mysql&job_direction=up&is_multi_write=false&is_use_sellout_info=true

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "node_types" : [ {
       "is_sellout" : false,
       "node_type" : "micro"
     }, {
       "is_sellout" : false,
       "node_type" : "small"
     }, {
       "is_sellout" : false,
       "node_type" : "medium"
     }, {
       "is_sellout" : false,
       "node_type" : "high"
     }, {
       "is_sellout" : false,
       "node_type" : "xlarge"
     } ]
   }

**Status code: 400**

Bad Request

.. code-block::

   {
     "error_code" : "DRS.M00202",
     "error_msg" : "The value of job_direction is invalid."
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
