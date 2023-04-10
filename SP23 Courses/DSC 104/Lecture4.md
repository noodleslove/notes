📕 Lecture #4
===

# The CAP Theorem (2000)
- consisency:
	- all nodes should see the same data at then smae time
- availability:
	- node failures do not revent survivors from continuing to operate
- partition-tolerance:
	- the system continues to operate despite network partitions
- theorem
	- a distributed system can satisfy any two of these guarantees at the same time.

## Implication of the CAP Theorem
- the CAP theorem suggests there are three kinds of distributed systems:
	- CP, AP, PA

## A More Realistic Idea
- AP systems relax consistency in favor of availability - but are not inconsistent
- CP systems sacrifice availability for consistency - but are not unavailable
- this suggetss both AP and CP systems can offer a degreee of consistency, and availability respectively, as well as partition tolerance

## Types of Consistency
- string ocnsistency
	- after the update completes, any subsequent access will return the same updated value
- weak consistency
	- it is not guaranteed that subsequent accesses will return the updated value
- eventual consistency
	- specific form of weak consistency
	- it is guaranteed that if no new updates are made to object, eventually all accesses will return the last updated value (e.g., progagate updates to replicas in a lazy fashion)

## BASE Systems
- as opposed to ACID
	- basically available, soft-state, eventually consistent
- basically available
	- the system is mostly "not down"
- soft-state
	- the situation taht information (state) the user put into the system that will go away if the user doesn't maintain it
		- the information will expire unless it is refreshed
		- in "hard-state" systems the user has to explicityly change state
	- another interpretation
		- the system may change state without active user input for eventual consistency

## Eventual Consistency Variations
- causal consistency
	- processes that have causal relationship will see consistent data
- read-your-write consistency
	- a process always accesses the data item after it's udate operation and never sees an older value
- session consistency
	- as long as session exists, system guarantees read-your-write consistency
	- guarantees do not overlap sessions
- monotonic read consistency
	- if a process has seen a particular value of data item, any subsequent processes will never return any previous values
- monotonic write consistency
	- the system guarantees to serialize the writes by the same process
- in practice
	- a number of these proporties can be combined
	- monotoic reads and read-your-writes are most desired


# Key-Value Store
- a key-value store can be viewed as a simple hash table
	- where all the accesses to the database are via primary keys
- a client can either:
	- get the value for a key
	- put a value for a key
	- delete a key from the data store
- it must exhibit high performance and availability
	- faster than creating two-column table in DBMS

# What can be put into a KV-Store?
- simplest case
	- a look-up table (e.g. country-name, cap)