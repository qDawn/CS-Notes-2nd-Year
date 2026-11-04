
- Divide and conquer algorithms break problems into smaller pieces
- They often split the input into equal sized pieces
- Some split and also look at interactions between pieces
- Key step is analyzing the running time using recurrence relations
- It can be used to speed up maths aswell 

## What is Divide and Conquer

- Divide: Break problems into several parts
- Conquer: Solve each part recursively
- Combine: Join solutions to sub problems into overall solutions

Most commonly used to obtain fast algorithms by splitting
- Break up problem of size n into two equal parts of size $\frac {1}{2}n$ 
- Solve two parts recursively
- Combine two solutions into overall solution in (near) linear time

Consequence of the splitting approach can be large e.g.
- Brute force for sorting/inversion counting: O($n^2$)
- Divide and conquer for these problems: O($nlogn$)

## Mergesort and Sorting

Sorting. Given n elements, rearrange in ascending order
There are many applications of sorting in computer science
- Some problems are inherently about sorting 
	- Sort a list of names
	- Display ranked search results
	- List news items in reverse chronological order
- Some problems become easier when their input is sorted
	- Find the median
	- Find the closest pair in 1 dimension
	- Binary search in a db
-  Some other problems rely on sorting in unexpected ways
	- Data compression
	- Computational biology
	- Load balacing on a parallel computer

## Mergesort Revisited

Mergesort is a divide and conquer sorting algorithm
- Divde array into two halves
- Recursively sort each half
- Merge two halves to make a sorted whole
![[Pasted image 20261104215845.png]]

### Merging

Combine two pre-sorted lists into a sorted whole

How to do it efficiently?
- Perform only a linear number of comparisons
- Use temporary array to build the merged output


## A Useful Recurrence Relation

Set T(n) = number of comparisons to mergesort an input of size n
We can calculate the Mergesort recurrence to define T(n)
- Base case: T(n) = 0 if n = 1 (signle elemtn list is already sorted)
- T(n) $\leq$ T($\frac{n}{2}$) + T($\frac{n}{2}$) + n otherwise Sort left half, sort right half, merge

Solution to the mergesort recurrence is T(n) = ($n\log_{2}n$)

To prove this recurrence
- Initially we assume n is a power of 2 for simplicity
- Then we have ($\frac{n}{2}$) + ($\frac{n}{2}$) = $\frac{n}{2}$


## Counting inversions

