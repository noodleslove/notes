📕 Lecture #8
===

# Column Family Databases
> column family -> a subset of columns that are likely to be accessed together

## Vertical Partitioning
- suppose we have a wide table
	- wide = many columns
- design questions
	- using a row-store is possibly wasteful
	- using a pure column-store will also be inefficient if most queries need joins
	- middle-of-the-road solution
		- break up the table "vertically"
		- keep "related" columns together
		- ensure table is still "re-constructable"

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

## Bond Energy Method
- from the attribute affinity (AA) matrix we will create a clustered affinity matrix (CA)
- general plan:
	- input: the AA matrix
	- output: the clustered affinity matrix CA which is a perturbation of AA
	- steps
		- initialization: place and fix one of the columns of AA in CA
		- iteration: place the remaining n-i columns in the remaining i+1 positions in the CA matrix. for each column, choose the placement that makes **the most contribution to the global affinity measure**.
		- row order: order rows according to the column ordering
