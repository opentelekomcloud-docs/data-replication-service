:original_name: drs_01_0007.html

.. _drs_01_0007:

Returned Values
===============

Status Code
-----------

After sending a request, you will receive a response, including a status code, response header, and response body.

A status code is a group of digits, ranging from 1xx to 5xx. It indicates the status of a request. For more information, see :ref:`Status Code <drs_api_0108>`.

For example, if status code 201 is returned for calling the API used to obtain a user token, the request is successful.

Response Header
---------------

Similar to a request, a response also has a header, for example, **Content-Type**.

:ref:`Figure 1 <drs_01_0007__en-us_topic_0117388900_fig85721224549>` shows the response header fields for the API used to obtain a user token is called. The **x-subject-token** header field is the desired user token. This token can then be used to authenticate the calling of other APIs.

.. _drs_01_0007__en-us_topic_0117388900_fig85721224549:

.. figure:: /_static/images/en-us_image_0000001782032750.png
   :alt: **Figure 1** Header fields of the response to the request for obtaining a user token

   **Figure 1** Header fields of the response to the request for obtaining a user token

Response Body
-------------

The body of a response is often returned in structured format as specified in the **Content-type** header field. The response body transfers content except the response header.

The following is part of the response body for the API used to obtain a user token. The following shows part of the response body for the API to obtain a user token.

.. code-block::

   {
       "token": {
           "expires_at": "2019-02-13T06:52:13.855000Z",
           "methods": [
               "password"
           ],
           "catalog": [
               {
                   "endpoints": [
                       {

                           "region_id": "eu-de",



   ......

If an error occurs during API calling, the system returns an error code and message to you. The following shows the format of an error response body:

.. code-block::

   {
       "error_msg": "The format of message is error",
       "error_code": "AS.0001"
   }

In the response body, **error_code** is an error code, and **error_msg** provides information about the error.
