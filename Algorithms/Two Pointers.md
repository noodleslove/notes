
# Tortoise and Hare

> The idea behind the algorithm is that, if you have two pointers in a linked list, one moving twice as fast (the hare) than the other (the tortoise), then if they intersect, there is a cycle in the linked list. If they don't intersect, then there is no cycle.


## Code

```Python
def hasCycle(head: Optional[Node]) -> bool:
	if not head or not head.next:
		return False

	tortoise = head
	hare = head.next;

	while hare and hare.next:
	    if tortoise === hare:
		    return True
    
	    tortoise = tortoise.next
	    hare = hare.next.next

	return False
```


## Showing How This Works

To help illustrate this algorithm, I'll use some very relevant clipart. We'll start with the linked list. The `tortoise` begins at the `head`, while the `hare` begins at `head.next`.

![Example 0](tortoise-and-hare-example_0.png)

Since `hare` and `hare.next` are both not `null`, we'll enter the while loop. `tortoise` and `hare` are not equal to each other, so we will move them both over. `tortoise` gets moved over one spot, and `hare` gets moved over two spots.

![Example 0](tortoise-and-hare-example_1.png)

The while loop is still true. Again, `tortoise` and `hare` are not equal to each other. We'll move the `tortoise` over one, and the `hare` over two nodes.

![Example 0](tortoise-and-hare-example_2.png)

The while loop is still true, but this time, `tortoise` and `hare` are equal to each other. This means that a cycle was found, so we will return true.


## Extras

When there exists a cycle, start a pointer `temp` and the start the linked list. Move both `tortoise` and `temp` over one at a time. When both pointers meet, there is the start of the cycle.
