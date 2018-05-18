# Algorithms and Data Structures

## Abstract Data Types

An abstract data type is defined in terms of abstract descriptions of data
that it contains and operations that it provides on that data.  A data structure,
on the other hand, is a more concrete description of the implementation of how
data is stored, and the algorithms that implement operations on that data.  Of
course, there are varying degrees of abstraction, so the line between these two
is not always clear, and even with data structures there may still be implementation
details that are not specified.

### Stack

### Queue

### Priority Queue

### Dictionary

### Graph

## Data Structures

### Array

### Linked List

Singly-linked and doubly-linked

### Binary Tree

* Each node has pointers to left and right child nodes, and optionally to parent
* Left is different from right (child nodes).
* Find the depth of a binary tree recursively, checking the depth of the left and 
  right subtrees, and adding one to whichever is greater.  The depth of an empty
  tree is 0.

### Binary Search Tree

* For any node x, all nodes in left subtree have value < x, and all nodes in
  right subtree have value > x
* There are versions where duplicate keys are allowed (say, where nodes in left subtree
  can be <= x), but this brings in complications, and most straightforward case is no
  duplicates allowed
* Can be balanced (AVL Tree and Red-Black Tree)
* For any given binary tree shape of n nodes, and n keys, there is exactly one way to assign
  each key to a node that will make the tree a binary search tree
* Minimum element is the left-most element, maximum is right-most element
* Three basic ways to traverse a BST -- in-order, pre-order, and post-order
* In-order traversal results in processing in sorted order
* In-order traversal: 1) process left subtree, 2) process item, 3) process right subtree
* There is only one place to insert a new value into a BST, which is the same place where
  we search for the value and find a null

### Heap

* Binary tree in which the key at each node "dominates" its children. For example, in
  a "min heap", each node is less than its child nodes.  Therefore, the top of the heap
  contains the minimum value.
* You can store the heap in an actual linked binary tree, or in an array.
* In the array version, the root is stored at position 1. Generally, left child of node
  at position k is stored at position 2k, and right node stored at position 2k + 1 (using
  a 1-based index).
* There is a way to keep the array completely filled, so you never waste any space.  Simply
  insert an element at the next (left-most) space, then if the dominance relationship with its
  parent isn't correct, just swap it with its parent, then continue looking at that parent, etc.
* To extract the minimum, just take the root.  Then, replace the root with the right-most leaf.
  Then, look at the new root and its two children, and if necessary, swap the new root with the
  minimum of its two children.  Then, continue in this way down the tree, until no swap is 
  necessary, or you swap an element into a leaf.
* The array version is more space-efficient, but you lose some flexibility in reorganizing
  the tree, and you cannot store arbitrary tree structures without wasting space. Typically,
  this tradeoff means that heaps can work well stored as an array, but binary search trees
  don't work so well as arrays.

### Hash Table

* Great data structure for implementing a dictionary
* Hash function -- takes a key and computes a hash key, typically an integer
* There is debate around ideal hash functions, and seems to be some "black magic"
  around creating them (i.e. specific procedures and constant values are used and
  are supposed to give good results without much theory around why they're supposed
  to work).
* Typically, it take O(m) time to compute a hash function on a string of length m
* If you have m buckets, to determine the (zero-based) bucket you take the outcome of
  the hash function and take it modulo m
* Need to handle collisions, most common way is to have linked lists at each array
  location.
* Hashing and hash tables are generally useful, for a wide variety of problems

### Kd-Tree

### B-Tree

### Skip List

### Trie

And Suffix Tree

### Adjacency Matrix

### Adjacency List

### Union Find

## Problems

Problems go here -- such as "minimum spanning tree" etc.  Time will tell if this is a useful category.

## Algorithms

### Sorting

* Sorting is useful for many problems, and can often form one part of the overall
  algorithm for solving a problem

Classic sorting algorithms:
* Selection Sort: Select the smallest element, swap it with the first element, continue
* Insertion Sort: Go through each element, insert it in the correct place in the list
* Heapsort: Create a heap by inserting one element at a time, then extract min n times.
* Mergesort: Sort two halves separately, then merge them by repeatedly picking smallest
* Quicksort: 

### Substring Search

* Problem: Given a string t and substring s, does t contain s, and if so, where?
* Rabin-Karp algorithm is a good one, which involves computing the hash of the
  substring s, and then the hash of each substring of t of length m (= length
  of s).  The trick is that it uses a "rolling hash" function which allows constant-
  time computation of hash at position i+1, when hash at position i is known. Any
  matches must be checked for collisions, which are hopefully rare.
* Actually, it appears there may be better algorithms, e.g. Boyer-Moore and
  Knuth-Morris-Pratt

### Algorithmic Tools

* Sorting
* Hashing / Hash Tables
* Recursion
* Incrementally building, one step at a time
* Breaking a problem down into smaller problems, then put the pieces together
* Dynamic Programming
* Greedy Algorithms






