## Interval Scheduling

- A schedule is a set of tasks which we call jobs. Each job has a start time $s_{i}$, and an end time $f_{i}$ Two jobs are compatible if they do not overlap

Problem:
- Find the most jobs you can possible have in a set time span

Potential Solution:
- Earliest start time
- Shortest Interval 
- Fewest conflicts
- earliest deadline

Optimal Solution:

<b>Earliest Deadline</b>  

Order jobs in terms of Earliest Finish Time and choose jobs which do not overlap

## Interval Partitioning

Problem:
 - Given a schedule of jobs j with start and finish time $s_{i}$ and $g_{i}$. We partition jobs into minimal amount of k resources such that no two jobs on the same resource overlap

Optimal Solution:
- Order Jobs by earliest start time

## Minimising Lateness

For p = prepare time and d = deadline given jobs j, what is the smallest amount of lateness you can achieve

Potential Solutions:
- Sort by prepare time
- Sort by slack time (d - p)
- 