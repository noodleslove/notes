📕 Lecture #8
===

# Column Family Databases
> column family -> a subset of columns that are likely to be accessed together

## Vertical Partitioning
- suppose we have a wide table
	- wide = many columns
- design questions
	- using a row-store is possibly wasteful
	- using a pure column-store 

## The Query Workload Estimation Exercise
- using our knowledge of the applications using the table
	- create a large collection of queries
		- large > 100
		- queries should not be similar
		- queries should represent the use cases of many different users
	- for each query
		- assign a query
		- frequency
			- 3% of all queries will be of type Q1, 7% of all queries will be of type Q2 ...
			- for every type of use-case
