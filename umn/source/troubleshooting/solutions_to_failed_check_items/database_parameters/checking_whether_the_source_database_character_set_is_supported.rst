:original_name: drs_03_043.html

.. _drs_03_043:

Checking Whether the Source Database Character Set Is Supported
===============================================================

Oracle Synchronization
----------------------

.. table:: **Table 1** Checking whether the source database character set is supported

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database character set is supported                                                                                                                                                                                    |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | If the character set of the source database is not supported, data synchronization may fail. A migration task from Oracle only supports the following character sets: ZHS16GBK, AL32UTF8, UTF8, US7ASCII, WE8MSWIN1252, and WE8ISO8859P1. |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The source database character set is not supported.                                                                                                                                                                        |
   |                                       |                                                                                                                                                                                                                                           |
   |                                       | Handling suggestion: Go back to the connection test page and select a source database with supported character sets or change the character set of the source database to AL32UTF8.                                                       |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
