## Sorting Algorithms

- Sorting is a fundamental algorithmic task
- From sorting contacts in a phone to massive scale data analytics
- .sort() in java and python are very handy

E.g:
- Bubble Sort
- Heap Sort
- Insertion Sort
- Radix Sort
- Quick Sort
- Merge Sort
- Selection Sort
- etc...

## Algorithmic perspectives on sorting

Various properties of sorting algorithms have been studied

- How many comparisons / swaps do they make?
- What is the worst case or average running time?
- What is the minimum time cost for any sorting algorithm?
- Is it stable? (keeps save values in the same order)
- What is the best sorting algorithm?

## Stable Matching 
### Theory
The idea is that you wish to match various types of entities with preferences. Such as doctors to hospitals or students to universities. 

## Goal 
Design a self enforcing admissions process such that there is no unstable pairs

## Unstable pairing
When say applicant A and Hospital H there exists an incident such that :
- A prefers H to their assigned hospital G
- And H refers D to one of their admitted students B

## Stable Assignment
When there are no unstable pairs
- Natural and desirable condition 
- Individual self-interest prevents any applicant/hospital swaps
- Need to show that a stable assignment exists and can be found

## Defining the Problem (summary)

- <b>Perfect matching</b> :
	- Each doctor gets assigned to one hospital
	- Each hospital gets exactly one new doctor
- <b>Stability</b> :
	- an unmatched pair A-H is unstable if doctor A prefers hospital H and H prefers doctor A.
	- Could improve by 'defecting'
- <b>Stable matching</b>:
	- perfect matching with no unstable pairs
- <b>Stable Matching Problem</b>
	- Given the preference lists of n doctors and hospitals find a stable matching if one exists

## Propose-And-Reject Algorithm

![[Pasted image 20261021194125.png]]

## Proof 

![[Pasted image 20261021194214.png]]
![[Pasted image 20261021194224.png]]![[Pasted image 20261021194301.png]]