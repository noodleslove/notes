📕 Lecture #18
===

## Indexing in MongoDB
- MongoDB creates a unique index on the \_id field during the creattion of a collection
- single key index
	- `db.products.createIndex({"category": 1})`
- compound indices
	- `db.products.createIndex({"category": 1, "item": 1})`
		- accessed for processing queries on either key (or both)
	- 