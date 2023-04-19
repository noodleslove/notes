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