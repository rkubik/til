# Index Summary

## Clustered vs. Non-Clustered

With a clustered index data is stored physically on the disk in the same order as
the index. Therefore only one clustered index can exist.

With a non clustered index there is a second list that has pointers to the
physical rows. You can have many non clustered indexes, however it will
increase the time it takes to write new records.

Generally:

1. Faster to read from clustered index if you want all columns.
2. Writing to a table with a clustered index can be slower, if there is a need
   to rearrange or reorder the data.


### Example with PostgreSQL

PostgreSQL does not have a concept of clustered indexes at all. Instead, all
tables are heap tables and all indexes are non-clustered indexes.

