:original_name: drs_11_0013.html

.. _drs_11_0013:

Checking Whether the Source and Destination Database Character Sets Are Consistent
==================================================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the source and destination database character sets are consistent

   +---------------------------------------+----------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source and destination database character sets are consistent                                      |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the character sets of the servers hosting the source and destination databases are consistent.   |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: This item cannot be checked because the source database fails to be connected.                  |
   |                                       |                                                                                                                |
   |                                       | Handling suggestion: Check whether the source database is connected.                                           |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: This item cannot be checked because the destination database fails to be connected.             |
   |                                       |                                                                                                                |
   |                                       | Handling suggestion: Check whether the destination database is connected.                                      |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Insufficient user permissions                                                                   |
   |                                       |                                                                                                                |
   |                                       | Handling suggestion: Check whether the database user permissions meet the migration requirements.              |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The character set of the source database is inconsistent with that of the destination database. |
   |                                       |                                                                                                                |
   |                                       | Handling suggestion: Modify the character sets.                                                                |
   |                                       |                                                                                                                |
   |                                       | Run commands to modify the self-created source database.                                                       |
   |                                       |                                                                                                                |
   |                                       | #. Check whether source and destination database character sets are consistent.                                |
   |                                       |                                                                                                                |
   |                                       |    .. code:: text                                                                                              |
   |                                       |                                                                                                                |
   |                                       |       show variables like "character_set_server"\G;                                                            |
   |                                       |                                                                                                                |
   |                                       |    |image1|                                                                                                    |
   |                                       |                                                                                                                |
   |                                       | #. Modify the character set of the source database server.                                                     |
   |                                       |                                                                                                                |
   |                                       |    .. code:: text                                                                                              |
   |                                       |                                                                                                                |
   |                                       |       set character_set_server='utf8';                                                                         |
   |                                       |                                                                                                                |
   |                                       |    |image2|                                                                                                    |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                       |
   |                                       |                                                                                                                |
   |                                       | Handling suggestion: Contact technical support.                                                                |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001391534273.png
.. |image2| image:: /_static/images/en-us_image_0000001341254040.png
