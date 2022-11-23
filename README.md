# Infrequent psql

A collection of PostgreSQL queries I only use occasionally.

## UUID extension
```sql
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
```

## UUID generate
```sql
CREATE TABLE foo (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4();
);
```


## Table size
```sql
SELECT pg_size_pretty(pg_relation_size('foo'));
```

## Tables by size
```sql
SELECT table_name,
       pg_relation_size(quote_ident(table_name)),
       pg_size_pretty(pg_relation_size(quote_ident(table_name)))
  FROM information_schema.tables
 WHERE table_schema = 'public'
 ORDER BY 2 DESC;
```

## Active connections
```sql
SELECT * FROM pg_stat_activity WHERE state = 'active' AND pid <> pg_backend_pid();
```

## Kill connection
```sql
SELECT pg_terminate_backend(pid);
```
