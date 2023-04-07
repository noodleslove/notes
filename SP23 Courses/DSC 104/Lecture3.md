
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
	- a node can be a master for some data and a s