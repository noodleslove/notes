📕 Lecture #9
===

## SSTable and MemTable
- MemTable
	- in-memory/write-back cache space consisting of the content in a key and column format
	- data in a memetable is sorted by key, and each column family consists of a distinct memtable that retrieves column data via the key
	- stores the writes until it is full, then flushes them out
- SSTable
	- accept regular written memtables
	- stored on disk and exist for each cassandra table
	- sstable do not allow any further additions or removal of data items once written
	- for each sstable, cassandra creates three separate files like partition index, partition summary, and a bloom filter to determine whether an object in a memtable is also in sstable

## A Heuristic Design
- nuber of items
	- $n = \text{ceil}(m / (-l / \text{log}(1 - \text{exp}((\text{log}(p) / k)))))$
- probability of false positive
	- $p = \text{pow}(1 - \text{exp}(-k / (m / n)), k)$
- number of bits
	- $m = \text{ceil}((n * \text{log}(p)) / \text{log}(1 / \text{pow}(2, \text{log}(2))))$
- number of hash functions
	- $k = \text{round}((m / n) * \text{log}(2))$

