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

## Data Can be Compressed
- some segments will compress more than others
- encoding/decoding

## Query Processing
- column elimination

## Downside
- accessing many of the columns in a table at once doesn't save much 
	- it could be more expensive than a row store
```sql
select *                        %%all columns%%
from long_wide_table
where order_line_id=321837291;  %%single row%%
```
- generally not ideal for tables with few columns
- update and deleting rows is expensive
	- some column stores are append only
	- others strongly discourage writes
	- some closed sourc column stores split storage into row and column areas

## Data Compression – Run-Length Encoding

## Data Compression – Bit-Vector Encoding

## Data Compression – Dictionary Encoding

## Data Compression – Frame of Reference Encoding
- the nature of data don't fluctuate much
- measure a frame of reference, then measure the difference afterwards

## Data Compression – Differential Encoding
- similar to frame of reference encoding
- multiple fix points

