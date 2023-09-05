```sql
SELECT * FROM pg_stat_replication;

SELECT * FROM pg_stat_subscription

SHOW wal_sender_timeout

SHOW max_replication_slots

SHOW max_wal_senders

SHOW max_worker_processes

SHOW max_logical_replication_workers

SHOW max_sync_workers_per_subscription;

SELECT * FROM pg_stat_bgwriter





SELECT * FROM pg_replication_slots
```

```


CREATE PUBLICATION ****;
GRANT rds_replication TO pub_user;
```

```

```

## Subscription

```
CREATE SUBSCRIPTION subscription_name
    CONNECTION 'conninfo'
    PUBLICATION publication_name [, ...]
    [ WITH ( subscription_parameter [= value] [, ... ] ) ]
```

##

A subscription represents a replication connection to the publisher.

this command normally creates a replication slot on the publisher

To find which tables might potentially include non-local origins (due to other subscriptions created on the publisher) try this SQL query:

```sql
# substitute <pub-names> below with your publication name(s) to be queried
SELECT DISTINCT PT.schemaname, PT.tablename
FROM pg_publication_tables PT,
     pg_subscription_rel PS
     JOIN pg_class C ON (C.oid = PS.srrelid)
     JOIN pg_namespace N ON (N.oid = C.relnamespace)
WHERE N.nspname = PT.schemaname AND
      C.relname = PT.tablename AND
      PT.pubname IN (<pub-names>);
```

## Publication

=

<https://www.postgresql.org/docs/current/sql-createpublication.html>

<https://www.postgresql.fastware.com/blog/inside-logical-replication-in-postgresql>

<https://www.morling.dev/blog/insatiable-postgres-replication-slot/>

<https://pgpedia.info/p/pg_wal_lsn_diff.html>

<https://wolfman.dev/posts/pg-logical-heartbeats/>
