
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

- Music site tries to match your song preferences with others
	- You rank n songs
	- Music site consults database to find people with similar tastes
- Similarity metric: number of inversions between two rankings
- If i > j then an inversion is needed there, 

## Applications of inversion counting 

The concept of inversions appear in many applications
- Voting theory to compare social choice
- Collaborative filtering 
- Measuring the "sortedness" of an array
- Sensitivity analysis of search engine ranking function
- Rank aggregation for meta searching on the web
- Computational biology, comparing two gene sequences
- Nonparametric statistics


## Divide and Conquer for inversion counting

- Divide: Separate list into two pieces
- Conquer: recursively count inversions in each half
- Combine: count inversions where $a_{i}$ and $a_j$ are in different halves and return sum of three quantities
![[Pasted image 20261105002127.png]]

Combine: count left-right inversions 
- Assume each half is sorted, and we will produce sorted output
- Count invesions where $a_i$ and $a_j$ are in different halves
	- How many items on left each one on the right has to 'leapfrog'
- Merge two sorted halves into sorted whole
![[Pasted image 20261105002748.png]]

## Implementation

![[Pasted image 20261105003131.png]]

# Closest pair of points

