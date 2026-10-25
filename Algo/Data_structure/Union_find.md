# Disjoint set - union find

## Definition

Disjoint sets are sets without any common elements.
Each set will have the presentative. 
By finding the presentative of a containing set, we can check if 2 elements linked to each other or not.

It will have these following operations:

* **Union** -> Combine 2 sets containing 2 elements ( if these 2 set are differ)
* **Find** -> To find the presentative of the set containing the elements

## Naive implementation

We will have a array of each elements's parents $parents[0], parents[1], \ldots, parents[n-1]$.
Now we will have set of virtual trees, each presenting a set.

The presentative of the set will have $parents[i] == i$.

To find, just trace up util we find the presentative. 
To union, just find the 2 presentatives , and set one to be the other's parent.


```java
void union(int a, int b) {

	int ap = find(a)
	int bp = find(b)
	
	if(ap != bp) {
		parents[ap] = bp;
	}
}

int find(int a) {
	if(a == parents[a] ) {
		return a;
	}
	
	return find(parents[a]);
}
```

For naive implementation, both operation's time complexity are $O(n)$, due to the tree's depth growing.
These following optimizations will help to reduce tree's depth.

## Path compression optimization

If we do **find** operation, we will link each elements to root directly. 
In the case below, after the `find(7)` operation, we will link each element `7`,`5`,`3`,`2` to `1`

![](../images/path-compression.png)

```java
int find(int a) {
	if(a == parents[a]) {
		return a;
	}
	
	int p = find(parents[a]);
	parents[a] = p;
	return p;
}
```

## Union by rank / size optimization

Instead of link the trees blindly in naive **Union**, 
we will find each tree's size / rank, then link the smaller one to the bigger one.

```java

void union(int a, int b) {

	int ap = find(a);
	int bp = find(b);
	
	if(ap != bp) {
		if(rank[a] == rank[b] ) {
			parent[b] = a;
			rank[a]++;
			return;
		}
		
		if(rank[a] > rank [b] ) {
			rank[b] = a;
		} else {
			rank[a] = b;
		}
	}
}

```