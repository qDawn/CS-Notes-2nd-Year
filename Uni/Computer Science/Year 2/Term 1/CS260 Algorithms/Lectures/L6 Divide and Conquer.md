
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

