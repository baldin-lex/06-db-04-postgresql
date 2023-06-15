# Домашнее задание к занятию 4. «PostgreSQL» - Балдин

## Задача 1

Используя Docker, поднимите инстанс PostgreSQL (версию 13). Данные БД сохраните в volume.

```bash
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE         COMMAND                  CREATED         STATUS         PORTS                                       NAMES
55c4361622c6   postgres:13   "docker-entrypoint.s…"   3 minutes ago   Up 3 minutes   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   baldin_pg
```

Подключитесь к БД PostgreSQL, используя `psql`.

```bash
[root@localhost ~]# docker exec -ti baldin_pg bash
root@55c4361622c6:/# psql -U baldin
psql (13.11 (Debian 13.11-1.pgdg120+1))
Type "help" for help.

baldin=# 
```

Воспользуйтесь командой `\?` для вывода подсказки по имеющимся в `psql` управляющим командам.

**Найдите и приведите** управляющие команды для:

- вывода списка БД
```bash
baldin=# \l
                              List of databases
Name    | Owner  | Encoding |  Collate   |   Ctype    | Access privileges 
-----------+--------+----------+------------+------------+-------------------
baldin    | baldin | UTF8     | en_US.utf8 | en_US.utf8 | 
postgres  | baldin | UTF8     | en_US.utf8 | en_US.utf8 | 
template0 | baldin | UTF8     | en_US.utf8 | en_US.utf8 | =c/baldin        +
          |        |          |            |            | baldin=CTc/baldin
template1 | baldin | UTF8     | en_US.utf8 | en_US.utf8 | =c/baldin        +
          |        |          |            |            | baldin=CTc/baldin
(4 rows)
```
- подключения к БД
```bash
baldin=# \conninfo
You are connected to database "baldin" as user "baldin" via socket in "/var/run/postgresql" at port "5432".
```
- вывода списка таблиц
```bash
baldin=# \dtS
                   List of relations
   Schema   |          Name           | Type  | Owner  
------------+-------------------------+-------+--------
 pg_catalog | pg_aggregate            | table | baldin
 pg_catalog | pg_am                   | table | baldin
 pg_catalog | pg_amop                 | table | baldin
 pg_catalog | pg_amproc               | table | baldin
 pg_catalog | pg_attrdef              | table | baldin
 pg_catalog | pg_attribute            | table | baldin
 pg_catalog | pg_auth_members         | table | baldin
 pg_catalog | pg_authid               | table | baldin
 pg_catalog | pg_cast                 | table | baldin
 pg_catalog | pg_class                | table | baldin
 pg_catalog | pg_collation            | table | baldin
 pg_catalog | pg_constraint           | table | baldin
 pg_catalog | pg_conversion           | table | baldin
 pg_catalog | pg_database             | table | baldin
 pg_catalog | pg_db_role_setting      | table | baldin
 pg_catalog | pg_default_acl          | table | baldin
 pg_catalog | pg_depend               | table | baldin
 pg_catalog | pg_description          | table | baldin
 pg_catalog | pg_enum                 | table | baldin
 pg_catalog | pg_event_trigger        | table | baldin
 pg_catalog | pg_extension            | table | baldin
 pg_catalog | pg_foreign_data_wrapper | table | baldin
 pg_catalog | pg_foreign_server       | table | baldin
 pg_catalog | pg_foreign_table        | table | baldin
 pg_catalog | pg_index                | table | baldin
 pg_catalog | pg_inherits             | table | baldin
 pg_catalog | pg_init_privs           | table | baldin
 pg_catalog | pg_language             | table | baldin
 pg_catalog | pg_largeobject          | table | baldin
 pg_catalog | pg_largeobject_metadata | table | baldin
 pg_catalog | pg_namespace            | table | baldin
 pg_catalog | pg_opclass              | table | baldin
 pg_catalog | pg_operator             | table | baldin
 pg_catalog | pg_opfamily             | table | baldin
 pg_catalog | pg_partitioned_table    | table | baldin
 pg_catalog | pg_policy               | table | baldin
 pg_catalog | pg_proc                 | table | baldin
 pg_catalog | pg_publication          | table | baldin
 pg_catalog | pg_publication_rel      | table | baldin
 pg_catalog | pg_range                | table | baldin
 pg_catalog | pg_replication_origin   | table | baldin
 pg_catalog | pg_rewrite              | table | baldin
 pg_catalog | pg_seclabel             | table | baldin
 pg_catalog | pg_sequence             | table | baldin
 pg_catalog | pg_shdepend             | table | baldin
 pg_catalog | pg_shdescription        | table | baldin
 pg_catalog | pg_shseclabel           | table | baldin
 pg_catalog | pg_statistic            | table | baldin
 pg_catalog | pg_statistic_ext        | table | baldin
 pg_catalog | pg_statistic_ext_data   | table | baldin
 pg_catalog | pg_subscription         | table | baldin
 pg_catalog | pg_subscription_rel     | table | baldin
 pg_catalog | pg_tablespace           | table | baldin
 pg_catalog | pg_transform            | table | baldin
 pg_catalog | pg_trigger              | table | baldin
 pg_catalog | pg_ts_config            | table | baldin
 pg_catalog | pg_ts_config_map        | table | baldin
 pg_catalog | pg_ts_dict              | table | baldin
 pg_catalog | pg_ts_parser            | table | baldin
 pg_catalog | pg_ts_template          | table | baldin
 pg_catalog | pg_type                 | table | baldin
 pg_catalog | pg_user_mapping         | table | baldin
(62 rows)
```
- вывода описания содержимого таблиц
```bash
baldin=# \dS+
                                           List of relations
   Schema   |              Name               | Type  | Owner  | Persistence |    Size    | Description 
------------+---------------------------------+-------+--------+-------------+------------+-------------
 pg_catalog | pg_aggregate                    | table | baldin | permanent   | 56 kB      | 
 pg_catalog | pg_am                           | table | baldin | permanent   | 40 kB      | 
 pg_catalog | pg_amop                         | table | baldin | permanent   | 80 kB      | 
 pg_catalog | pg_amproc                       | table | baldin | permanent   | 64 kB      | 
 pg_catalog | pg_attrdef                      | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_attribute                    | table | baldin | permanent   | 456 kB     | 
 pg_catalog | pg_auth_members                 | table | baldin | permanent   | 40 kB      | 
 pg_catalog | pg_authid                       | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_available_extension_versions | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_available_extensions         | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_cast                         | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_class                        | table | baldin | permanent   | 136 kB     | 
 pg_catalog | pg_collation                    | table | baldin | permanent   | 248 kB     | 
 pg_catalog | pg_config                       | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_constraint                   | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_conversion                   | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_cursors                      | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_database                     | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_db_role_setting              | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_default_acl                  | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_depend                       | table | baldin | permanent   | 488 kB     | 
 pg_catalog | pg_description                  | table | baldin | permanent   | 376 kB     | 
 pg_catalog | pg_enum                         | table | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_event_trigger                | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_extension                    | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_file_settings                | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_foreign_data_wrapper         | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_foreign_server               | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_foreign_table                | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_group                        | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_hba_file_rules               | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_index                        | table | baldin | permanent   | 64 kB      | 
 pg_catalog | pg_indexes                      | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_inherits                     | table | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_init_privs                   | table | baldin | permanent   | 56 kB      | 
 pg_catalog | pg_language                     | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_largeobject                  | table | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_largeobject_metadata         | table | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_locks                        | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_matviews                     | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_namespace                    | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_opclass                      | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_operator                     | table | baldin | permanent   | 144 kB     | 
 pg_catalog | pg_opfamily                     | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_partitioned_table            | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_policies                     | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_policy                       | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_prepared_statements          | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_prepared_xacts               | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_proc                         | table | baldin | permanent   | 688 kB     | 
 pg_catalog | pg_publication                  | table | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_publication_rel              | table | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_publication_tables           | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_range                        | table | baldin | permanent   | 40 kB      | 
 pg_catalog | pg_replication_origin           | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_replication_origin_status    | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_replication_slots            | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_rewrite                      | table | baldin | permanent   | 656 kB     | 
 pg_catalog | pg_roles                        | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_rules                        | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_seclabel                     | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_seclabels                    | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_sequence                     | table | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_sequences                    | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_settings                     | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_shadow                       | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_shdepend                     | table | baldin | permanent   | 40 kB      | 
 pg_catalog | pg_shdescription                | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_shmem_allocations            | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_shseclabel                   | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_stat_activity                | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_all_indexes             | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_all_tables              | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_archiver                | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_bgwriter                | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_database                | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_database_conflicts      | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_gssapi                  | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_progress_analyze        | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_progress_basebackup     | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_progress_cluster        | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_progress_create_index   | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_progress_vacuum         | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_replication             | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_slru                    | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_ssl                     | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_subscription            | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_sys_indexes             | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_sys_tables              | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_user_functions          | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_user_indexes            | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_user_tables             | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_wal_receiver            | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_xact_all_tables         | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_xact_sys_tables         | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_xact_user_functions     | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stat_xact_user_tables        | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_statio_all_indexes           | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_statio_all_sequences         | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_statio_all_tables            | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_statio_sys_indexes           | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_statio_sys_sequences         | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_statio_sys_tables            | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_statio_user_indexes          | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_statio_user_sequences        | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_statio_user_tables           | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_statistic                    | table | baldin | permanent   | 248 kB     | 
 pg_catalog | pg_statistic_ext                | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_statistic_ext_data           | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_stats                        | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_stats_ext                    | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_subscription                 | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_subscription_rel             | table | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_tables                       | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_tablespace                   | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_timezone_abbrevs             | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_timezone_names               | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_transform                    | table | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_trigger                      | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_ts_config                    | table | baldin | permanent   | 40 kB      | 
 pg_catalog | pg_ts_config_map                | table | baldin | permanent   | 56 kB      | 
 pg_catalog | pg_ts_dict                      | table | baldin | permanent   | 48 kB      | 
 pg_catalog | pg_ts_parser                    | table | baldin | permanent   | 40 kB      | 
 pg_catalog | pg_ts_template                  | table | baldin | permanent   | 40 kB      | 
 pg_catalog | pg_type                         | table | baldin | permanent   | 120 kB     | 
 pg_catalog | pg_user                         | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_user_mapping                 | table | baldin | permanent   | 8192 bytes | 
 pg_catalog | pg_user_mappings                | view  | baldin | permanent   | 0 bytes    | 
 pg_catalog | pg_views                        | view  | baldin | permanent   | 0 bytes    | 
(129 rows)
```

- выхода из psql
```bash
baldin=# \q
root@55c4361622c6:/# 
```
---

## Задача 2

Используя `psql`, создайте БД `test_database`.

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/virt-11/06-db-04-postgresql/test_data).

Восстановите бэкап БД в `test_database`.

Перейдите в управляющую консоль `psql` внутри контейнера.

Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.

Используя таблицу [pg_stats](https://postgrespro.ru/docs/postgresql/12/view-pg-stats), найдите столбец таблицы `orders` 
с наибольшим средним значением размера элементов в байтах.

**Приведите в ответе** команду, которую вы использовали для вычисления, и полученный результат.

## Задача 3

Архитектор и администратор БД выяснили, что ваша таблица orders разрослась до невиданных размеров и
поиск по ней занимает долгое время. Вам как успешному выпускнику курсов DevOps в Нетологии предложили
провести разбиение таблицы на 2: шардировать на orders_1 - price>499 и orders_2 - price<=499.

Предложите SQL-транзакцию для проведения этой операции.

Можно ли было изначально исключить ручное разбиение при проектировании таблицы orders?

## Задача 4

Используя утилиту `pg_dump`, создайте бекап БД `test_database`.

Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца `title` для таблиц `test_database`?

---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
