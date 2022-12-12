:original_name: drs_08_0001.html

.. _drs_08_0001:

Parameters for Comparison
=========================

Parameter comparison helps you check consistency between the source and destination database data to ensure your services will not be affected after being migrated.

This section lists the common parameters and performance parameters of different DB engine versions for your reference during parameter comparison.

MySQL 5.6
---------

.. table:: **Table 1** MySQL 5.6 parameters to be compared

   =============================== ===================== ================
   Parameter                       Type                  Restart Required
   =============================== ===================== ================
   connect_timeout                 Common parameter      No
   event_scheduler                 Common parameter      No
   innodb_lock_wait_timeout        Common parameter      No
   max_connections                 Common parameter      No
   net_read_timeout                Common parameter      No
   net_write_timeout               Common parameter      No
   explicit_defaults_for_timestamp Common parameter      Yes
   innodb_flush_log_at_trx_commit  Common parameter      No
   max_allowed_packet              Common parameter      No
   tx_isolation                    Common parameter      No
   character_set_client            Common parameter      No
   character_set_connection        Common parameter      No
   collation_connection            Common parameter      No
   character_set_results           Common parameter      No
   collation_server                Common parameter      No
   binlog_cache_size               Performance parameter No
   binlog_stmt_cache_size          Performance parameter No
   bulk_insert_buffer_size         Performance parameter No
   innodb_buffer_pool_size         Performance parameter Yes
   key_buffer_size                 Performance parameter No
   long_query_time                 Performance parameter No
   query_cache_type                Performance parameter Yes
   read_buffer_size                Performance parameter No
   read_rnd_buffer_size            Performance parameter No
   sort_buffer_size                Performance parameter No
   sync_binlog                     Performance parameter No
   =============================== ===================== ================

MySQL 5.7
---------

.. table:: **Table 2** MySQL 5.7 parameters to be compared

   =============================== ===================== ================
   Parameter                       Type                  Restart Required
   =============================== ===================== ================
   connect_timeout                 Common parameter      No
   event_scheduler                 Common parameter      No
   innodb_lock_wait_timeout        Common parameter      No
   max_connections                 Common parameter      No
   net_read_timeout                Common parameter      No
   net_write_timeout               Common parameter      No
   explicit_defaults_for_timestamp Common parameter      No
   innodb_flush_log_at_trx_commit  Common parameter      No
   max_allowed_packet              Common parameter      No
   tx_isolation                    Common parameter      No
   character_set_client            Common parameter      No
   character_set_connection        Common parameter      No
   collation_connection            Common parameter      No
   character_set_results           Common parameter      No
   collation_server                Common parameter      No
   binlog_cache_size               Performance parameter No
   binlog_stmt_cache_size          Performance parameter No
   bulk_insert_buffer_size         Performance parameter No
   innodb_buffer_pool_size         Performance parameter No
   key_buffer_size                 Performance parameter No
   long_query_time                 Performance parameter No
   query_cache_type                Performance parameter No
   read_buffer_size                Performance parameter No
   read_rnd_buffer_size            Performance parameter No
   sort_buffer_size                Performance parameter No
   sync_binlog                     Performance parameter No
   =============================== ===================== ================

.. note::

   The value of **innodb_buffer_pool_size** is set to not exceed 70% of the total memory of the destination database. If you set a larger value for the parameter, the destination database startup may fail. Therefore, values of **innodb_buffer_pool_size** in the source and destination databases are different. You can adjust the value to suit your services.
