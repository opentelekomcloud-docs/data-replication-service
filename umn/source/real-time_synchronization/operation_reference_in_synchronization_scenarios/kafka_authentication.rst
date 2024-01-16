:original_name: drs_05_0018.html

.. _drs_05_0018:

Kafka Authentication
====================

PLAINTEXT
---------

No security authentication mode is available. You only need to enter the IP address and port for connection.


.. figure:: /_static/images/en-us_image_0000001710630028.png
   :alt: **Figure 1** PLAINTEXT

   **Figure 1** PLAINTEXT

.. _drs_05_0018__section14347513434:

SASL_PLAINTEXT
--------------

The SASL mechanism is used to connect to Kafka, and you need to configure SASL parameters.


.. figure:: /_static/images/en-us_image_0000001758429637.png
   :alt: **Figure 2** SASL_PLAINTEXT

   **Figure 2** SASL_PLAINTEXT

.. table:: **Table 1** Parameter settings

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                   |
   +===================================+===============================================================================================================================================================+
   | SASL Mechanisms                   | SASL is used by client. The following four items are supported. Kafka server uses the GSSAPI mechanism by default.                                            |
   |                                   |                                                                                                                                                               |
   |                                   | -  GSSAPI                                                                                                                                                     |
   |                                   | -  PLAIN                                                                                                                                                      |
   |                                   | -  SCRAM-SHA-256                                                                                                                                              |
   |                                   | -  SCRAM-SHA-512                                                                                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Token Delegation                  | Whether an agency token is used for authentication. This option is available when **SCRAM-SHA-256** or **SCRAM-SHA-512** is selected for **SASL Mechanisms**. |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Username                          | Username for logging in to the database                                                                                                                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Password                          | Password for the username                                                                                                                                     |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _drs_05_0018__section83072273310:

SSL
---

SSL is used to encrypt the connection to Kafka. Related parameters need to be configured.


.. figure:: /_static/images/en-us_image_0000001758549461.png
   :alt: **Figure 3** SSL

   **Figure 3** SSL

.. table:: **Table 2** Parameter settings

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                                |
   +===================================+============================================================================================================================================================================================================+
   | Truststore Certificate            | SSL certificate with the file name extension .jks.                                                                                                                                                         |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Truststore Certificate Password   | Password of the certificate                                                                                                                                                                                |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Endpoint Identification Algorithm | Endpoint identification algorithm for verifying the host name of the server using the server certificate. This parameter is optional. If this parameter is left blank, host name verification is disabled. |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Mutual SSL Authentication         | Mutual SSL Authentication                                                                                                                                                                                  |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Keystore Certificate              | If mutual SSL authentication is enabled, you need to upload the mutual SSL authentication certificate with the file name extension .jks.                                                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Keystore Certificate Password     | Password of the mutual SSL authentication certificate. This option is available if mutual SSL authentication is enabled.                                                                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Keystore Private Key Password     | (Optional) Password of the private key in the keystore certificate.                                                                                                                                        |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

SASL_SSL
--------

If the SASL and SSL are used, configure SSL and SASL parameters. For details, see :ref:`SASL_PLAINTEXT <drs_05_0018__section14347513434>` and :ref:`SSL <drs_05_0018__section83072273310>`.


.. figure:: /_static/images/en-us_image_0000001758549465.png
   :alt: **Figure 4** SASL_SSL

   **Figure 4** SASL_SSL
