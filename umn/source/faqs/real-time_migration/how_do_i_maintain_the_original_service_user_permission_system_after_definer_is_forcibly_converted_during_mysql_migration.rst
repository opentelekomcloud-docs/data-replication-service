:original_name: drs_16_0003.html

.. _drs_16_0003:

How Do I Maintain the Original Service User Permission System After Definer Is Forcibly Converted During MySQL Migration?
=========================================================================================================================

Definer is used in views, stored procedures, triggers, and events. Definer does not restrict the permission to invoke objects, instead the permission to access the database. If you select **Yes** for **Migrate Definer to User** during MySQL migration, the Definers of all source database objects will be migrated to the user. The user continues to use the original services without authorization. (Users, permissions, and passwords are migrated). Other users do not have permissions on database objects unless these users are authorized.

The following procedures describe how to use database commands to authorize users.

#. Ensure that the new user (Definer uses the specified account) has sufficient permission to execute view- and stored procedure-related SQL statements.

#. Log in to the destination database using the MySQL official client or other tools.

#. Run the following command to view details about permissions of the user to be authorized:

   .. code-block:: text

      show grants for  'user'@'host';

#. To ensure that the original service does not report an error, run the following command to grant the user the operation permissions the involved database objects do not have:

   .. code-block:: text

      grant select,insert,update,delete on db_name.* to 'user'@'host';

   Generally, the permissions to access the database are as follows: SELECT, CREATE, DROP, DELETE, INSERT, UPDATE, INDEX, EVENT, CREATE VIEW, CREATE ROUTINE, TRIGGER, and EXECUTE. You need to check the permissions that are missing based on the database object, and then perform the authorization operation.

   For stored procedures and functions, ensure that the user has the EXECUTE permission. The authorization command is as follows:

   .. code-block:: text

      grant execute on db_name.function_name to 'user'@'host';

#. Use the authorized account to access the destination database. If the access is successful, the authorization is successful. Note: If the following information is displayed when a stored procedure or function is invoked in a Java project, the **mysql.proc** database must be authorized: Java.sql.SQLException: User does not have access to metadata required to determine stored procedure parameter types. If rights can not be granted, configure connection with "noAccessToProcedureBodies=true" to have driver generate parameters that represent INOUT strings irregardless of actual parametertypes

   .. code-block:: text

      grant select on mysql.proc to 'user'@'host';
