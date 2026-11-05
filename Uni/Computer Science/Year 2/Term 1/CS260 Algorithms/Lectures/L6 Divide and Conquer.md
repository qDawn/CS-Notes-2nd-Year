
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

Given n points in the plane, find a pair with smallest euclidean distance between them

Closest pair is a fundamental geometric primitve:
- Graphics, games, computer vision, geographic information systems, molecular modeling, air traffic control
- Special case of nearest neighbour, Euclidean MST, Voronoi diagrams
	- Fast closest pair inspired fast algorithms for these problems

Brute force: check all pairs of points p,q with O($n^2$) comaprisons
Assumption No two points have the same x coordinate

## Algorithm for closest pair

Divide: draw vertical line L so that roughly $\frac{1}{2}n$ points on each side
Conquer: find closest pair in each side recursively
Combine: find closeest pair with one point in each side

![[Pasted image 20261105004512.png]]

Find the closest pair with a point in each side, assuming distance < $\delta$ 
- Observation: only need to consider points with $\delta$ of line L 
- Sort points in $2\delta$ strip by their y coordinate
- Only check distances of those within 7 positions in sorted list
- This is because it doesn't make sense to check that far as its obviously longer in $\delta$ + y distance, there is a proof that there is at most 7 other points in this supposed box
![[Pasted image 20261105011719.png]]
![[Pasted image 20261105011802.png]]

## Analysis

For the running time the recurrence relation can be written as such
$$ T(n) = 2T\left( \frac{n}{2} \right) + O(n\log n)$$

Base case: T(1) = O(1)
- We can solve this by recursion tree or telescoping to get T(n) = $O(n\log^2n)$ 

$O(n\log n)$ is possible with a more involved solution
- Don't sort points in strip 
- Each recursive call returns two lists: all points sorted by y coordinate for the strip and x coordinate for the line L
- Get the new lists by merging the two pre-sorted lists

# Master Method

