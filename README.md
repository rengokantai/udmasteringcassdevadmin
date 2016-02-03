#### udmasteringcassdevadmin
- cp6 config
```
systemctl start cassandra
systemctl enable cassandra
nodetool status
```
- cp8
create a keyspace
```
CREATE KEYSPACE vt WITH replication = {'class': 'SimpleStrategy', 'replication_factor': '1'}  AND durable_writes = true;
```

create table.first use keyspace
```
use vt;
```
then
```
CREATE TABLE vt.a (
    id text,
    datetime timestamp,
    event text,
    PRIMARY KEY (id, datetime)
) WITH CLUSTERING ORDER BY (datetime DESC)
```
