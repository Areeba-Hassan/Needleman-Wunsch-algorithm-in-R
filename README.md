This R project implements the Needleman-Wunsch algorithm for global sequence alignment.

What’s the Needleman-Wunsch algorithm?

It’s a powerful algorithm that uses dynamic programming to find the optimal alignment between two sequences. It is widely used in bioinformatics for DNA, RNA, and protein sequence alignment, and helps researchers identify regions of similarity between sequences to provide insights into evolutionary relationships or functional regions of genes.

Here’s a breakdown of its core components:

1. The Scoring Matrix:
The Scoring matrix computes scores for each pair of characters (letters in a sequence), based on matches, mismatches, and gaps. A match scores positively, a mismatch scores negatively, and gaps costs a penalty. The matrix is designed so that it aligns two sequences in multiple ways for optimization. 

Here’s an example of optimal alignment with two sequences: ATGC and ATC.

One possible alignment can be:

ATGC
 | | x _
ATC

Another one could be:

ATGC
 | | _ |
AT  C

Here, alignment no. 2 is optimal with 3 matches and one gap, whereas alignment 1 is less favorable with 2 matches, a gap and a mismatch. This optimal alignment is determined by the traceback function

2. Traceback:
After filling the matrix, the algorithm traces back through it to reveal the best sequence alignment. The traceback stars from the bottom right cell and tracks all the way up to the first cell of the matrix, and in this way determines the optimal path.

Now, for the implementation. It is as simple as it gets!

For two sequences of length n and m, a matrix of size (n+1) x (m+1) is created and initialized with matrix[n*-2, 1] and matrix[1, m*-2]

To fill the matrix, three paths are considered for a cell [n, m]:
[n, m-1] (left; represents gap)
[n-1, m] (up; represents gap)
[n-1, m-1] (diagonal; represents a match or a mismatch)
The match/mismatch score or the gap penalties are added to the values in each direction. The maximum of the resultants fills [n, m]

The traceback uses recurrence to track all the directions that were followed to generate an alignment, while also calculating the alignment score by summing all matches, substitutions and deletions.
