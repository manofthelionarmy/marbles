[Links?](#)
[Embbed Videos?](#)
[Partition Pruning - Postgres Docs](https://www.postgresql.org/docs/current/ddl-partitioning.html#DDL-PARTITION-PRUNING)
# Summary

----
# Related Stuff

----
# Notes:
- Partitions allow us to logically split a large table into chunks.
- If we don't enable partition pruning, then each partition will be scanned for whatever value we are looking for.
- When partition pruning is enabled, the optimizer will select the correct partition.

## Questions:

## Follow Up:
