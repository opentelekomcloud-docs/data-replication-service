:original_name: drs_05_0002.html

.. _drs_05_0002:

Abnormal Request Results
========================

-  Abnormal response description

   .. table:: **Table 1** Abnormal response description

      +------------+--------+--------------------------------------------------------------------------------------------------------------------------------+
      | Name       | Type   | Description                                                                                                                    |
      +============+========+================================================================================================================================+
      | error_code | String | Specifies the error code returned when the API response is abnormal. For details, see section :ref:`Error Code <drs_05_0004>`. |
      +------------+--------+--------------------------------------------------------------------------------------------------------------------------------+
      | error_msg  | String | Specifies the description of the error returned when the API response is abnormal.                                             |
      +------------+--------+--------------------------------------------------------------------------------------------------------------------------------+

-  Example Response:

   .. code-block:: text

      {
          "error_code": "DRS.M00201",
          "error_msg": "The %s parameter is empty."
      }
      {
          "error_code": "DRS.M00202",
          "error_msg": "The value of %s is invalid."
      }
