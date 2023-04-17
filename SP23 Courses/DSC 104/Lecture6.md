📕 Lecture #6
===

# Column and Column-Family Stores

## Suppose we have the following Workload Information
- many more read operations compared to write operations
	- high query to update ratio
- many more concurrent reads comparedto concurrent writes
	- applications not transaction-heavy
- the number of columns is large
	- wide table
- most queries access a small fraction of the columns
- typical queries have GROUP BY and aggregate operations

## Consider Column Stores
- row group
	- set of rows (typically 1 million)
- column segment
	- contains values from one column from the row group
- segements are compressed
- each segement stored separately
- segment is unit of transfer between disk and memeory

## A Column is the Stored Object

## Column Store Characteristics
- operating on columns enables and/or is combined with the following optimizations:
	- compression
		- compress values per column
	- late tuple materialization
		- construct tuples as late as possible
	- block iteration
		- pass blocks of values between operators
	- invisible join

## Why Compression?
advantages of compression in general:
- lower storage space requirements
- better I/O performance
	- read fewer data (from disk, SSD, or RAM) gain from cache locality
- better query processing perfromance
	- typically when operating directly on compressed data
