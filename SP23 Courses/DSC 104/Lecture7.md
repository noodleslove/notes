📕 Lecture #7
===

## Scalability of DBMS
- variants:
	- amount of data
	- query complexity

## "Early" Tuple Materialization
- read relevant columns & create tuple
- run query at a tuple level as usual

## Late Tuple Materialization
- create tuple as late in the plan as possible

## Bit Vectors and RLE
- how do we do the AND operation?
- option 1: use bit vectors
- option 2: use RLE

## Benefits of Late Materialization
- avoid materialzing certain tuples
	- since they may be filtered out before being materialized
	- (reminds of pushing selections down)
- avoid data decompression
	- which has to be done when a tuple is materialized
- leverage improved cache locality
	- which exists when operating on a single column
- leverage optimizations for fixed-width attributes
	- which would not be possible if operating on the tuple level one variable-width attribute becomes variable-width

## Block Iteration
> pipeline paralleling: process tuples one by one with parallelism. 
- row store
	- pass single tuples between operators
	- extract attribute value through function calls
- column store
	- pass blocks of values between operators
	- no need for attribute extraction

## Hybrid Stores
- for many opeartions, late materialization-based joins are significantly faster than early materialization-based joins
- in some column-stores (e.g., HP Vertica)
	- a row-store AND a column-store are maintained
	- tuples are migrated from one to the other as needed
	- ingestion is slower but retrieval is very fast
