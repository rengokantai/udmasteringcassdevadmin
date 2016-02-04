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

- cp9
copy from(copy csv to table), copy to(copy table content to csv)  
we create a table a.csv:
```
id,datetime,event
22,1993-01-01 11:22:22,fsd
```
Then copy to table a  
```
cqlsh:vt> copy a(id,datetime,event)from '/root/a.csv' with header=true and delimiter=',';
```

create index  
```
cqlsh:vt> create index aindex on a(datetime);
```


- cp11
using TTL (second), time to live
```
INSERT INTO a(id,datetime,event)values('20','2016-01-01 12:12:12','eventc') using TTL 30;
```
