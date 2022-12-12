:original_name: drs_12_0001.html

.. _drs_12_0001:

How Can I Import Users and Permissions from the Source to the Destination Database?
===================================================================================

#. Log in to an ECS that can access the source database.

#. Run the following command, enter the password as prompted, and press **Enter** to export the source database users to the **users.sql** temporary file:

   **mysql** **-h** *'host'* **-u** *'user'* **-p** ``-``\ **N $@ -e** "SELECT CONCAT('SHOW GRANTS FOR ''', user, ``'''@''',`` host, ''';') AS query FROM mysql.user" > **/tmp/users.sql**

   **host** indicates the IP address of the source database and **user** indicates the username of the source database.

#. Run the following command to export the authorization information of the users from the source database to the **grants.sql** file:

   **mysql** **-h** *'host'* **-u** *'user'* **-p** -**N $@ -e** **"source /tmp/users.sql"** > **/tmp/grants.sql**

   **sed -i** **'s/$/;/g' /tmp/grants.sql**

   **host** indicates the IP address of the source database and **user** indicates the username of the source database.

#. .. _drs_12_0001__en-us_topic_0000001160149236_li102520718167:

   After the preceding command has been executed successfully, open the **grants.sql** file. Information similar to the following is displayed:

   .. code-block::

      -- Grants for root@%
      GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';

      -- Grants for testt@%
      GRANT SELECT, INSERT, UPDATE, DELETE ON *.* TO 'testt'@'%';

      -- Grants for debian-sys-maint@localhost
      GRANT ALL PRIVILEGES ON *.* TO 'debian-sys-maint'@'localhost' WITH GRANT OPTION;

      -- Grants for mysql.session@localhost
      GRANT SUPER ON *.* TO 'mysql.session'@'localhost';
      GRANT SELECT ON `performance_schema`.* TO 'mysql.session'@'localhost';
      GRANT SELECT ON `mysql`.`user` TO 'mysql.session'@'localhost';

      -- Grants for mysql.sys@localhost
      GRANT USAGE ON *.* TO 'mysql.sys'@'localhost';
      GRANT TRIGGER ON `sys`.* TO 'mysql.sys'@'localhost';
      GRANT SELECT ON `sys`.`sys_config` TO 'mysql.sys'@'localhost';

      -- Grants for root@localhost
      GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;
      GRANT PROXY ON ''@'' TO 'root'@'localhost' WITH GRANT OPTION;

#. The information displayed in :ref:`4 <drs_12_0001__en-us_topic_0000001160149236_li102520718167>` shows all users of the source database and their permissions. Add the required users one by one to the RDS MySQL database on the current cloud.
