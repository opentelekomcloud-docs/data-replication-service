:original_name: drs_14_0004.html

.. _drs_14_0004:

How Do I Change the Destination Database Password to Meet the Password Policy?
==============================================================================

Scenarios
---------

When you set the password for the migration account in the destination database, you need to set the password based on the password strength requirements of the destination database.

Procedure
---------

The following operations apply to the scenario where the target database is an RDS instance.

#. Log in to the RDS console.

#. Locate the target DB instance.

#. Click the DB instance name.

#. On the **Basic Information** page, click the **Parameters** tab.

#. .. _drs_14_0004__en-us_topic_0000001160467846_li21254109563:

   Enter the keyword **password** in the search box in the upper right corner of the page and press **Enter** to view the search result.

#. In the search result in :ref:`5 <drs_14_0004__en-us_topic_0000001160467846_li21254109563>`, change the values of the parameters listed in :ref:`Table 1 <drs_14_0004__en-us_topic_0000001160467846_table1711716281411>` based on the password strength requirements. Ensure that the parameter values are within the password complexity range.

   .. _drs_14_0004__en-us_topic_0000001160467846_table1711716281411:

   .. table:: **Table 1** Password description

      +--------------------------------------+---------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                            | Allowed Value       | Description                                                                                                                           |
      +======================================+=====================+=======================================================================================================================================+
      | validate_password_length             | 0-2,147,483,647     | Specifies the minimum password length verified by the validate_password plugin.                                                       |
      +--------------------------------------+---------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | validate_password_mixed_case_count   | 0-2,147,483,647     | Specifies the minimum number of lowercase and uppercase letters in a password when the password policy level is **MEDIUM** or higher. |
      +--------------------------------------+---------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | validate_password_number_count       | 0-2,147,483,647     | Specifies the minimum number of digits in a password when the password policy level is **MEDIUM** or higher.                          |
      +--------------------------------------+---------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | validate_password_policy             | LOW, MEDIUM, STRONG | Specifies the password policy executed by the validate_password plugin.                                                               |
      +--------------------------------------+---------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | validate_password_special_char_count | 0-2,147,483,647     | Specifies the minimum number of non-alphanumeric characters in a password when the password policy level is **MEDIUM** or higher.     |
      +--------------------------------------+---------------------+---------------------------------------------------------------------------------------------------------------------------------------+

#. After the parameter values are modified, save the modification.

#. Back to the **Select Migration Type** page and perform the next step.
