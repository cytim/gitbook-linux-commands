# PostgreSQL

### Turn On the Expanded Table Formatting Mode

```
\x
```

### Describe Table Structure

```
\d+ <SCHEMA_NAME>.<TABLE_NAME>
```

### Estimate the Total Number of Rows

```sql
SELECT schemaname, relname, n_live_tup FROM pg_stat_all_tables WHERE relname='<TABLE_NAME>';
```

### Check Query State

```sql
SELECT state, query FROM pg_stat_activity WHERE query LIKE '<QUERY_PATTERN>';
```
