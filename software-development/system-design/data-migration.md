# Data Migration

When an application grows, there are chances that we need to update the data model to improve the database performance
or to fit the new business requirements. For example, we might need to break down a giant database into smaller shards
<sup>[1]</sup>, or extract a table column into its own table <sup>[2]</sup>.

After the new design is settled, we will migrate the data from the old setup to the new one. The migration takes 4 steps
usually <sup>[1]</sup>.

1. **Double-write**: Apply the incoming write transactions to both the old and new data sink.
2. **Backfill**: Migrate the old data to the new data sink.
3. **Verification**: Make sure the data is 100% the same on both the old and new data sink.
4. **Switch-over**: Use the new data sink as the production data source.

## Migration Plan

### 1. Double-write

There are a few solutions for double-writing to multiple data sinks. One or more solutions maybe applicable depending on
the situation.

- **Database replication.** There are many tools to help migrate data between databases. However, this is only
  applicable when migrating data without structural changes.

- **The application writes to both data sinks directly.** A simple solution, but the drawback is that there could be
  many failing cases that cause the data sinks to out-sync. For example, a transaction could have been successful in one
  data sink but failed in another.

- **Write a catch-up script to track the transaction log.** This is the most flexible and reliable way to double-write.
  The script might have to omit the "update" transactions if a record does not exist yet. The record will be backfilled
  in the backfilling step. A more performant catch-up script can reduce the maintenance window during the switch-over.

### 2. Backfill

Backfilling is done by another script to copy the existing records from the old data sink to the new one. The script
should compare the record version that it won't overwrite the data from double-write.

### 3. Verification

Verifying the data integrity gives you the confidence that the migration scripts are working as expected. It is
suggested that the migration scripts and the verification scripts are written by different people.

- **A sampling script** is a script to compare the records from both data sinks randomly.

- **"Dark mode" reading<sup>[2]</sup>** is an implementation to double-read from both data sinks and compare the data
  on-the-fly when the consumers request them.

### 4. Switch-over

Switch-over means using the new data sink for both primary read and write. Unless eventual consistency is acceptable, a
maintenance window is required to switch-over because the double-write strategy usually takes a while to catch up with
the old data sink.

## Fallback Plan

When we switch-over, we should keep the old data sink in-sync with the new one. Then we can be safe to fallback to the
old data sink any time.

## References

1. [Herding elephants: Lessons learned from sharding Postgres at Notion](https://www.notion.so/blog/sharding-postgres-at-notion)
2. [Re-architecting Slack’s Workspace Preferences: How to Move to an EAV Model to Support Scalability](https://slack.engineering/re-architecting-slacks-workspace-preferences-how-to-move-to-an-eav-model-to-support-scalability/)
