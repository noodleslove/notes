
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