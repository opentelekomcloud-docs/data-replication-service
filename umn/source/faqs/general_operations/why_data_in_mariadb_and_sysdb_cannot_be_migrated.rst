:original_name: drs_16_0122.html

.. _drs_16_0122:

Why Data in MariaDB and SysDB Cannot Be Migrated?
=================================================

In some MariaDB versions, the SysDB database is used as a system database (similar to the sys database of MySQL 5.7). Therefore, DRS considers the SysDB database as the system database of all MariaDB databases by default (similar to the MySQL, information_schema, and performance_schema databases). If the SysDB is a service database, you can apply for a service ticket.
