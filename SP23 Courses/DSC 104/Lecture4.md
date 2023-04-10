
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
