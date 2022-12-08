:original_name: drs_16_0121.html

.. _drs_16_0121:

What Can I Do If the Invoking Permission Problem Occurs After the MySQL Stored Procedure Is Migrated to the Cloud?
==================================================================================================================

After the MySQL stored procedure is migrated to the cloud, an error may occur when the stored procedure or function is invoked due to permission problems.

The method varies with Definer policies. This section uses user1 as an example to describe how to solve this problem in two Definer policies.

.. _drs_16_0121__en-us_topic_0000001160467748_section612283113595:

**Policy 1**
------------

On the **Destination Database** page, enter the database username **user1**, and select **OK** for **Migrate Definer to User**.

In this policy, after the Definers of all stored procedures and methods in the source database are migrated to the destination database, the account is automatically changed to user1, and the value of host is automatically changed to %. If a stored procedure fails to be invoked in the destination database, perform the following operations:

#. Log in to the RDS MySQL DB instance of the destination database as the user1.

#. Grant the execute permission to the account that you want to use to invoke a stored procedure.

#. Run the following statement to use user1 to grant other accounts the permission to execute stored procedures:

   **user** indicates other accounts that need to invoke the stored procedure.

   .. code-block:: text

      GRANT EXECUTE ON db.* TO user;

#. To invoke a stored procedure using Java, run the following statement to use user1 to grant other accounts the permission to query the **mysql.proc** table:

   The following is the authorization statement, in which **user** indicates the account that needs to invoke the stored procedure:

   .. code-block:: text

      GRANT SELECT ON mysql.proc TO 'user'@'%';

**Policy 2**
------------

On the **Destination Database** page, enter the database username **user1**, and select **Cancel** for **Migrate Definer to User**.

In this policy, the account and host in the source database remain unchanged after the Definers of all stored procedures and methods are migrated to the destination database. You need to migrate all users in the source database by referring to :ref:`Migrating Accounts <drs_09_0017>`. In this way, the permission system of the source database remains unchanged.

If you do not migrate account permissions or some accounts cannot be migrated, you are advised to use :ref:`Policy 1 <drs_16_0121__en-us_topic_0000001160467748_section612283113595>`.
