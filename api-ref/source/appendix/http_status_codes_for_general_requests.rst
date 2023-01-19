:original_name: drs_05_0003.html

.. _drs_05_0003:

HTTP Status Codes for General Requests
======================================

-  Normal

   .. table:: **Table 1** Return codes for successful requests

      +-------------+-------------------------------------------------------------------------------+
      | Status Code | Description                                                                   |
      +=============+===============================================================================+
      | 200         | Request succeeded.                                                            |
      +-------------+-------------------------------------------------------------------------------+
      | 202         | Asynchronous requests (such as performing a task) are submitted successfully. |
      +-------------+-------------------------------------------------------------------------------+

-  Abnormal

   .. table:: **Table 2** Return codes for failed requests

      +------------------------------+-------------------------------------------------------------------------------------+
      | Status Code                  | Description                                                                         |
      +==============================+=====================================================================================+
      | 400 Bad Request              | The server fails to process the request.                                            |
      +------------------------------+-------------------------------------------------------------------------------------+
      | 401 Unauthorized             | You must enter the username and password to access the requested page.              |
      +------------------------------+-------------------------------------------------------------------------------------+
      | 403 Forbidden                | You are forbidden to access the page requested.                                     |
      +------------------------------+-------------------------------------------------------------------------------------+
      | 404 Not Found                | The server could not find the requested page.                                       |
      +------------------------------+-------------------------------------------------------------------------------------+
      | 405 Method Not Allowed       | The method specified in the request is not allowed.                                 |
      +------------------------------+-------------------------------------------------------------------------------------+
      | 409 Conflict                 | The request cannot be processed due to conflicts.                                   |
      +------------------------------+-------------------------------------------------------------------------------------+
      | 413 Request Entity Too Large | The request exceeds the resource quota.                                             |
      +------------------------------+-------------------------------------------------------------------------------------+
      | 415 Unsupported Media Type   | **Content-Type** contained in the request header is not **application/json**.       |
      +------------------------------+-------------------------------------------------------------------------------------+
      | 422 Unprocessable Entity     | Parameter or object in the request cannot be identified.                            |
      +------------------------------+-------------------------------------------------------------------------------------+
      | 500 Internal Server Error    | Failed to complete the request. The server is abnormal.                             |
      +------------------------------+-------------------------------------------------------------------------------------+
      | 501 Not Implemented          | Failed to complete the request. The server does not support the requested function. |
      +------------------------------+-------------------------------------------------------------------------------------+
      | 503 Service Unavailable      | Failed to complete the request. The system is currently unavailable.                |
      +------------------------------+-------------------------------------------------------------------------------------+
