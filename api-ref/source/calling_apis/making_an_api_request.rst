:original_name: drs_01_0008.html

.. _drs_01_0008:

Making an API Request
=====================

This section describes the structure of a REST API request, and uses the IAM API for `obtaining a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__ as an example to demonstrate how to call an API. The obtained token can then be used to authenticate requests for calling other APIs.

Request URI
-----------

A request URI consists of the following parts:

**{URI-scheme}://{Endpoint}/{resource-path}?{query-string}**

.. table:: **Table 1** Request URI

   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter     | Description                                                                                                                                                                                                                                                       |
   +===============+===================================================================================================================================================================================================================================================================+
   | URI-scheme    | Protocol used to transmit requests. All APIs use HTTPS.                                                                                                                                                                                                           |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Endpoint      | Domain name or IP address of the server bearing the REST service endpoint. Obtain the value from `Regions and Endpoints <https://docs.otc.t-systems.com/endpoint/index.html>`__.                                                                                  |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource-path | API access path for performing a specified operation. Obtain the path from the URI of an API. For example, the **resource-path** of the API used to obtain a user token is **/v3/auth/tokens**.                                                                   |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | query-string  | Query parameter, which is optional. Ensure that a question mark (?) is included before each query parameter that is in the format of "Parameter name=Parameter value". For example, **? limit=10** indicates that a maximum of 10 data records will be displayed. |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Request Method
--------------

The HTTP protocol defines the following request methods that can be used to send a request to the server.

.. table:: **Table 2** Request Method

   +--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Method | Description                                                                                                                               |
   +========+===========================================================================================================================================+
   | GET    | Requests a server to return specified resources.                                                                                          |
   +--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | PUT    | Requests a server to update specified resources.                                                                                          |
   +--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | POST   | Requests a server to add a resource or perform special operations.                                                                        |
   +--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | DELETE | Requests a server to delete specified resources, for example, an object.                                                                  |
   +--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | HEAD   | Same as GET except that the server must return only the response header.                                                                  |
   +--------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | PATCH  | Requests a server to update partial content of a specified resource. If the resource does not exist, the PATCH method creates a resource. |
   +--------+-------------------------------------------------------------------------------------------------------------------------------------------+

For example, in the case of the API used to obtain a user token, the request method is POST. The request is as follows:

.. code-block:: text

   POST https://iam.eu-de.otc.t-systems.com/v3/auth/tokens

Request Headers
---------------

You can also add additional header fields to a request, such as the fields required by a specified URI or HTTP method. For example, to request for the authentication information, add **Content-Type**, which specifies the request body type.

:ref:`Table 3 <drs_01_0008__en-us_topic_0117388899_table1999891313010>` describes common request headers need to be added to requests.

.. _drs_01_0008__en-us_topic_0117388899_table1999891313010:

.. table:: **Table 3** Common request headers

   +-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------+
   | Name            | Description                                                                                                                                                                                        | Mandatory                               | Example                                                                                         |
   +=================+====================================================================================================================================================================================================+=========================================+=================================================================================================+
   | Content-Type    | Specifies the MIME type of the request body.                                                                                                                                                       | Yes                                     | The default value is **application/json**. Other values will be described in the specific APIs. |
   +-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------+
   | Content-Length  | Length of the request body. The unit is byte.                                                                                                                                                      | -  Optional for POST or PUT requests.   | 3495                                                                                            |
   |                 |                                                                                                                                                                                                    | -  Must be left blank for GET requests. |                                                                                                 |
   +-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------+
   | X-Auth-Token    | Specifies a user token. This field is mandatory when token authentication is used. User token is a response to the API for obtaining a user token (only this API does not require authentication). | Yes                                     | ``-``                                                                                           |
   +-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------+
   | X-Language      | Request language type.                                                                                                                                                                             | No                                      | en-us                                                                                           |
   +-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------+-------------------------------------------------------------------------------------------------+

.. note::

   For details about other headers, see the HTTP protocol.

The API used to obtain a user token does not require authentication. Therefore, only the **Content-Type** field needs to be added to requests for calling the API. An example of such requests is as follows:

.. code-block:: text

   POST https://iam.eu-de.otc.t-systems.com/v3/auth/tokens
   Content-Type: application/json

Request Body
------------

The body of a request is often sent in a structured format as specified in the **Content-Type** header field. If the request body contains full-width characters, these characters must be coded in UTF-8.

The request body varies between APIs. Some APIs do not require the request body, such as the APIs requested using the GET and DELETE methods.

In the case of the API used to obtain a user token, the request parameters and parameter description can be obtained from the API request. The following provides an example request with a body included. Replace **username**, **domainname**, **\*******\*** (login password), and **xxxxxxxxxx** (project ID, for example, eu-de) with the actual values. To learn how to obtain a project ID, see `Regions and Endpoints <https://docs.otc.t-systems.com/endpoint/index.html>`__.

.. note::

   The **scope** parameter specifies where a token takes effect. You can set **scope** to an account or a project under an account. You can set scope to an account or a project under an account. For details, see `Obtaining a User Token Through Password Authentication <https://docs.otc.t-systems.com/api/iam/en-us_topic_0057845583.html>`__.

.. code-block::

   POST https://iam.eu-de.otc.t-systems.com/v3/auth/tokens
   Content-Type: application/json

   {
       "auth": {
           "identity": {
               "methods": [
                   "password"
               ],
               "password": {
                   "user": {
                       "name": "username",
                       "password": "********",
                       "domain": {
                           "name": "domainname"
                       }
                   }
               }
           },
           "scope": {
               "project": {
                   "name": "xxxxxxxxxxxxxxxxxx"
               }
           }
       }
   }

If all data required for the API request is available, you can send the request to call the API through `curl <https://curl.haxx.se/>`__, `Postman <https://www.getpostman.com/>`__, or coding. In the response to the API used to obtain a user token, **x-subject-token** is the desired user token. You can use the token to authenticate other API calls.
