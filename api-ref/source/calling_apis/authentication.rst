:original_name: drs_01_0005.html

.. _drs_01_0005:

Authentication
==============

You can use the following authentication method:

Token authentication: Requests are authenticated using tokens.

Token Authentication
--------------------

.. note::

   The validity period of a token is 24 hours. When using a token for authentication, cache it to prevent frequently calling the IAM API used to obtain a user token.

A token specifies temporary permissions in a computer system. During API authentication using a token, the token is added to requests to get permissions for calling the API.

In section :ref:`3.1 Making an API Request <drs_01_0008>`, the process of calling the API used to obtain a user token is described. After a token is obtained, add the **X-Auth-Token** header field must be added to requests to specify the token when calling other APIs. For example, if the token is **ABCDEFJ....**, **X-Auth-Token: ABCDEFJ....** can be added to a request as follows:

.. code-block:: text

   GET https://iam.eu-de.otc.t-systems.com/v3/auth/projects
   Content-Type: application/json
   X-Auth-Token: ABCDEFJ....
