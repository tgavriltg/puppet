这个主要是puppet的一些配置管理，其中主要包括一些mysql和redis的配置，这两个的配置是在同一个nood下同时启动多个deamon的配置。
下面是在同一个nood的配置：
node 'client.test.com'{
	redis_single::redis{'6379':port=>6379,masterip=>'172.16.2.4'}
	redis_single::redis{'6479':port=>6479,masterip=>'172.16.2.4'}
        mysql_server::percona{'3306':
                port                            => 3306,
                ensure                          => 'running',
                type                            => 'master',
                innodb_buffer_pool_size         => '8G',
                max_connections                 => 512,
                max_heap_table_size             => '16M',
                read_buffer_size                => '4M',
                read_rnd_buffer_size            => '8M',
                sort_buffer_size                => '4M',
                join_buffer_size                => '4M',
                query_cache_size                => '16M',
                innodb_flush_log_at_trx_commit  => 0
        }
        mysql_server::percona{'3307':
                port                            => 3307,
                ensure                          => 'running',
                type                            => 'master_candidate',
                innodb_buffer_pool_size         => '8G',
                max_connections                 => 128,
                max_heap_table_size             => '16M',
                read_buffer_size                => '4M',
                read_rnd_buffer_size            => '4M',
                sort_buffer_size                => '4M',
                join_buffer_size                => '4M',
                query_cache_size                => '32M',
                innodb_flush_log_at_trx_commit  => 0
        }
        mysql_server::percona{'3309':
                port                            => 3309,
                ensure                          => 'running',
                type                            => 'slave_myisam',
                innodb_buffer_pool_size         => '3G',
                max_connections                 => 512,
                max_heap_table_size             => '16M',
                read_buffer_size                => '4M',
                read_rnd_buffer_size            => '4M',
                sort_buffer_size                => '16M',
                join_buffer_size                => '4M',
                query_cache_size                => '32M',
                key_buffer_size                 => '3G',
                innodb_flush_log_at_trx_commit  => 0
        }
}
