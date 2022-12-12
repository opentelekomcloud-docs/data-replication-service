:original_name: drs_09_0017.html

.. _drs_09_0017:

Migrating Accounts
==================

Scenarios
---------

During a database migration, accounts need to be migrated separately.

MySQL Databases Operations
--------------------------

During the migration of MySQL databases, there are accounts that can be migrated completely, accounts whose permissions need to be reduced, and accounts that cannot be migrated.

-  Accounts that can be completely migrated refer to the accounts that meet the permission requirements of the destination database. By default, the system automatically migrates the permission of the database account to the destination database.

-  Accounts whose permissions need to be reduced refer to high-level accounts that fail to meet the permission requirements of the destination database, such as super, file, and shutdown. To migrate these accounts, reduce the permissions of the account. Otherwise, the migration fails.

   You can click **View** in the **Remarks** column to view detailed information about the permission to be reduced. You can then determine whether the permission reduction will have an impact on your services.

-  Accounts that cannot be migrated indicate that database users cannot meet the migration requirements for certain reasons. These accounts will not be migrated to the destination database. Ensure that services are not affected by these accounts. After the migration is started, any operation of changing the password or permission for these accounts will result in an incremental migration failure.

You can choose whether to migrate the accounts. Perform the following operations to set the database username, permission, and password. The following procedure uses all database users that can be migrated as an example.

The account information consists of account name, permission, and password.

#. The account name is in the **'Account name'+@+'host'** format. **host** indicates the IP address of the destination database, which is allowed to access the source database. You can change the IP address as required.

#. By default, account permissions cannot be modified. For accounts that can be migrated (including accounts that can be completely migrated and accounts whose permissions need to be reduced), the system also migrates the permissions of these accounts.

   After the migration is successful, accounts in the destination database are those whose permissions need to be reduced.

#. Migrate account passwords.

   You can use either of the following methods to migrate account passwords:

   DRS does not check your password strength during migration so you should set a strong password to ensure data security.

   Method 1: Migrate the password.

   You can directly migrate the current password of the source system. In this case, you do not need to select **Reset Password**. After the passwords are migrated to the destination database, you can set a strong password to ensure database security.

   Method 2: Reset the password.

   You can select **Reset Password** to reset the password of the source system and then continue the password migration.

   You can enter new passwords in the **Passwords** column for specified accounts that can be migrated, or select all accounts that can be migrated and select **Set Unified Password** to set a unified new password for them. After the migration is successful, you can run DDL statements on the destination database to reset the password.

#. For accounts whose permissions need to be reduced and accounts that cannot be migrated, you can click **View** to confirm the remarks before performing the next step. If there are multiple accounts, you can click **Confirm All Remarks**.

   If an account already exists in the destination database, it cannot be migrated. You can delete it from the destination database. After the deletion, you can continue the migration.

   .. note::

      -  The new password you set must meet the password policy of the destination database. For details, see :ref:`How Do I Change the Destination Database Password to Meet the Password Policy? <drs_14_0004>`

MongoDB Database Operations
---------------------------

During the migration of MongoDB databases, accounts to be migrated can be classified into the following types: accounts that can be migrated completely and accounts that cannot be migrated.

You can choose whether to migrate the accounts. If you need to migrate the accounts, perform the following procedures.

The account information consists of account name and role.

#. Select the accounts and roles to be migrated based on service requirements.

   If the account to be migrated depends on some roles, you must migrate the roles. Otherwise, the migration fails.

#. For accounts or roles that cannot be migrated, you can click **View** to confirm the remarks before performing the next step. If there are multiple accounts, you can click **Confirm All Remarks**.
