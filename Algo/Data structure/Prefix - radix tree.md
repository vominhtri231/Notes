# Definition
Prefix tree (Trie) and radix tree are used to saved arrays or strings, make searching for string faster. 

* A prefix tree (or a trie) is a binary tree where each letter is saved in a node.  

```
      ()
    /    \
   J      M
  / \     |
 O   A    A 
 |   |    |
 H   N    X
 |   |
 N   E         
```

* A radix tree is the compressed form of prefix tree. It saves the common letters in one node.

```
     ()
    /  \
   J   MAX
  / \ 
OHE ANE         
```

=> There are 3 strings JOHN, JANE, MAX are saved in those trees above
