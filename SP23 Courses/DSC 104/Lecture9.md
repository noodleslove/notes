📕 Lecture #9
===

## SSTable and MemTable
- MemTable
	- in-memory/write-back cache space consisting of the content in a key and column format
	- data in a memetable is sorted by key, and each column family consists of a distinct memtable that retrieves column data via the key
	- stores the writes until it is full, then flushes them out
- SSTable
	- accept regular 