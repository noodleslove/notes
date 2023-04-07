📕 Lecture #3
===


## Distribution Models: Sharding

We should try to ensure that 
- Data accessed together is kept together

### Master-slave Replication

- we replicate data across multiple nodes
- one node is designated as primary (master), other as secondary (slave)
- for scaling a read-intensive application
	- more read requests -> more slave nodes
	- the master fails -> the slaves can still handle read requests
	- a slave can become a new master quickly (it is a replica)
- limited by ability of the master to process updates
- masters are selected manually or automartically
	- user-defined vs. electe by the cluster manager

### Peer-to-peer Repilcation

- no master, all the replicas are equal
- every node can handle a write and then spreads the update to others
- problem: consistency
	- users can write simultaneously at two different nodes
- solution:
	- when writing, the replicas coordinate to avoid conflict
		- at the cost of networ traffic
		- the write operation waits till the coordination process is finished
	- not all replicas need to agree on the write, just a majority


## Sharding & Replication

- sharding and master-slave replication:
	- each data shard is replicated (via a single master)
	- a node can be a master for some data and a slave for other data
- sharding and peer-to-peer replication
	- a common strategy for column-family databases
		- a typical default is replication factor of 3
			- each shard is present on 3 nodes

### Replication Consistency

- consistency among replicas
	- ensuring that the same data item has the same value when reading from different replicas
	- after some time, the write propagates everywhere
- **eventual consistency**, meanwhile: stale data
	- various levels of consistency
	- read-your-writes (session consistency)
	- is violated if one user writes and reads on different replicas
	- solution: sticky session (session affinity)
		- requests for a particular session to the smae physical machine that serviced the first request for that session

### Quorums

- peer-to-peer replication with replication factor $N$
	- number of replicas of each data objeect
- read quorum: R
	- number of peers contacted for a single read
		- assuming that each value has a timestamp (time of write) to tell the older value from the newer
	- for a strong read consistency: $R + W > N$
		- reader surely does not read stale data
