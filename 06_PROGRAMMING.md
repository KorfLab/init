Programming Practice
====================

To be useful in my lab, you must be a competent programmer. How do you know if
you are and how do you get there if you are not? "Programming 0-60" is a list
of programming tasks that covers basic Python. You should be able to complete
all of these tasks by yourself (without AI). "Practical Programming" is a list
of more complex programming projects that are typical of what you might
encounter as a bioinformatics programmer.

- Programming 0-60
- Practical Programming


Programming 0-60
================

Rules:

- No imports are allowed unless explicitly stated
- Follow KorfLab style guide (80 columns, tab indents, etc.)

Variable naming conventions:

- `x` by itself can represent anything, but often a float
- `i`, `j`, `k`, and loop variables
- `n` and `m` are integers
- `a`, `b`, and `c` are numbers (sometimes ints, sometimes floats)
- `x`, `y`, and `z` are floats and often Cartesian coordinates
- `x1`, `y1` and `x2`, `y2` are Cartesian pairs
- `p` and `q` are probabilities
- `s` is a string, as are `s1` and `s2`
- `c` by itself is a character (e.g. `for c in s`)
- `strings` is a list of strings as are `strings1` and `strings2`
- `X` is a list of numbers, as are `X1` and `X2`
- `P` and `Q` are probability distributions (histograms)
- `nt` is a character representing a nucleotide
- `dna` is a string of nucleotide symbols
- `aa` is a character representing an amino acid
- `pro` is a string of amino acids
- `seq` is a string of nucleotides or amino acids
- `seqs` is a list of sequences
- `file` is a named file path
- `fp` is a file pointer

------------------------------------------------------------------------------

## Programs 0-20

### Output

0. Write a program `hello.py` that prints "hello world" to the terminal.

1. Write a program `maths.py` that assigns variables, performs some math
operations, and prints the results. For example, assign variables `a` and `b`,
calculate the hypotenuse `c`, and print the results.

2. Write a program `ascii.py` that prints out the ASCII decimal values for `A`
and `a` separated by a comma.

3. Write a program `bits.py` that prints the base 2 logarithm of pi and e to 5
digits of precision. Separate the values with a tab. Use `math.log2()`,
`math.pi`, and `math.e`.

### Functions with one parameter

4. Write a function `ftoc(x)` that converts Fahrenheit to Celsius. 32F equals
0C and 212F equals 100C.

5. Write a function `mph_to_kph(x)` that converts miles per hour to kilometers
per hour. There are 0.62137 miles in a kilometer.

6. Write a function `is_int(x)` that determines (returns Boolean) if the input
parameter is equal to an integer (has remainder 0 when divided by 1).

7. Write a function `is_prob(x)` that determines (returns Boolean) if a number
is a valid probability (x >= 0 and x <= 1).

8. Write a function `complement(nt)` that returns the complement of a DNA
letter.

9. Write a function `phred_to_prob(c)` that converts a PHRED quality symbol
into an error probability.

10. Write a function `prob_to_phred(p)` that converts a probability into a
PHRED quality symbol.

### Functions with multiple parameters

11. Write a function `pythagoras(a, b)` that returns the hypotenuse of a right
triangle with sides of length a and b.

12. Write a function `max3(a, b, c)` that returns the maximum of 3 numbers. You
my not use the `max()` function or any list methods.

13. Write a function `distance(x1, y1, x2, y2)` that computes the Cartesian
distance between two points on a graph.

### 1D iteration over range

14. Write a function `triangular(n)` that returns the triangular number (the
sum of the integers from 1 to n) for a non-negative integer.

15. Write a function `factorial(n)` that returns the factorial of a
non-negative integer.

16. Write a function `is_prime(n)` that determines (returns Boolean) if an
integer is a prime number.

17. Write a program `fizzprime.py` that prints the numbers from 1 to 100. If
the number is divisible by 3 print Fizz instead. If it is divisible by 5 print
Buzz instead. If it is divisible by both, print FizzBuzz instead. If the number
is prime, immediately follow the output with a `*`.

18. Write a program `fibonacci.py` that prints out the first 100 numbers of the
Fibonacci sequence.

19. Write a program `euler.py` that estimates the value of e (2.71828...) by
computing the infinite sum of 1/n!. Stop the calculation when the estimate runs
out of precision (repeats the same value twice). Print the current estimate
each time through the loop. You may use `math.factorial()`.

20. Write a program `nilakantha.py` that estimates Pi using the Nilakantha
series (Pi = 3 + 4/2x3x4 - 4/4x5x6 + 4/6x7x8 ...). Terminate the loop when
upper and lower bounds are within 1e-6 of the actual value. Print the current
estimate each time through the loop.

------------------------------------------------------------------------------

## Programs 21-40

### 1D iteration over data

21. Write a function `gc_comp(dna)` that returns the GC composition of a
nucleotide sequence. Use the `input()` function  to ask the user for a sequence
and then report its GC composition.

22. Write a function `oligo_tm(dna)` that computes the melting temperature of a
DNA sequence. For oligos <= 13 nt, Tm = (A+T) x 2 + (G+C) x 4. For longer
oligos, Tm = 64.9 + 41 x (G+C -16.4) / (A+T+G+C). Use the `sys.argv` as the
source of the DNA sequence.

23. Write a program `crazycase.py <file>` that converts a file into aLtErNaTiNg
cAsE. Use `sys.argv` to get the file name.

24. Write a function `anti(nt)` that returns the reverse-complement of a DNA
sequence.

25. Write a function `entropy(P)` that returns the entropy of a probability
distribution. The function should check that `P` sums to 1 and report an error
if this is not the case.

26. Write a function `maxstr(strings)` that returns the string with the longest
length in a list of strings.

27. Write a function `minstrlen(strings)` that returns the length of the
shortest string in a list of strings.

### Multiple Return Values

28. Write a function `minmax(X)` that returns the minimum and maximum values
from a list of numbers. You may not use `max()`, `min()`, or list methods.

29. Write a function `stats(X)` that returns the mean, standard deviation, and
median for a list of numbers.

30. Write a program `colorname.py <file> <R> <G> <B>` that reports the closest
official HTML color name given some RGB values on the command line. Data is in
the `colors_extended.tsv` file.

### Parallel Traversal

31. Write a function `percent_id(s1, s2)` that computes the percent identity
between two strings of equal length (e.g. a pairwise sequence alignment).

32. Write a function `manhattan(X1, X2)` that computes the Manhattan distance
between two lists of numbers.

33. Write a function `dkl(P, Q)` that computes the Kullback-Leibler distance
between two histograms. You should check that P and Q are actually histograms
and you should do _something_ about values of zero.

### List Search

34. Write a program `jaccard.py <file1> <file2>` that computes the Jaccard
Index (intersection divided by union) for 2 files of names. Create your own
file data to test your program.

35. Write a function `hydropathy(pro)` that computes the average Kyte-Doolitle
hydrophobicity of a protein sequence. Use the variables as defined below.

```
aas = 'ACDEFGHIKLMNPQRSTVWY'
kdh = (1.8, 2.5, -3.5, -3.5, 2.8, -0.4, -3.2, 4.5, -3.9, 3.8, 1.9, -3.5, -1.6,
	-3.5, -4.5, -0.8, -0.7, 4.2, -0.9, -1.3)
```

36. Write a function `translate(dna)` that translates a nucleotide sequence
into a protein sequence. If the codon is partial or has ambiguity symbols,
translate to X. Use the variables defined below. The variable `codons` is a
list of all possible codons `AAA`, `AAC`, `AAG`, `AAT`, `ACA`, ... `TTT` in
alphabetical order.

```
codons = [''.join(t) for t in itertools.product('ACGT', repeat=3)]
trans = 'KNKNTTTTRSRSIIMIQHQHPPPPRRRRLLLLEDEDAAAAGGGGVVVV*Y*YSSSS*CWCLFLF'
```

### Monte Carlo

37. Write a program `monty-pi-thon.py` that estimates Pi by throwing random
darts at Cartesian quadrant 1. Let it run infinitely. For inspiration see
https://en.wikipedia.org/wiki/Monte_Carlo_method

38. Write a function `random_dna(n, X=[0.25, 0.25, 0.25, 0.25])` that returns a
random DNA sequence of length n. The optional named parameter `X` allows the
caller to specify weights for A, C, G, and T sequentially.

39. Write a function `random_subseq(seq, n, k)` that randomly samples a
sequence, returning a list of `n` sub-sequences of length `k`.

40. Write a function `mutate(dna, p)` that randomly mutates a DNA sequence
given some probability `p` of mutation.

------------------------------------------------------------------------------

## Programs 41-60

### 2D Loops

41. Write a program `print_matrix.py <alphabet> <plus> <minus>` that displays a
simple scoring matrix for matches and mismatches. The program must have the
alphabet and scores as command line arguments. Given the command line shown,
the output should match exactly.

```
python3 print_matrix.py ACGT +1 -1
   A  C  G  T
A +1 -1 -1 -1
C -1 +1 -1 -1
G -1 -1 +1 -1
T -1 -1 -1 +1
```

42. Write a program `triples.py <n>` that finds all Pythagorean Triples with
sides from 1 to `n` (e.g. 100). There should be no duplicates. For example,
3-4-5 is a Pythagorean Triple, but 4-3-5 is really the same thing and should
not be reported.

43. Write a program `birthday1.py <c> <n>` that simulates the birthday paradox
(the probability that two people in a classroom have the same birthday is > 50%
once the class size is 23 or more). Use a list for the people, not the
calendar. `c` and `n` represent the size of the calendar (e.g. 365) and number
of people (e.g. 23).

44. Write a program `birthday2.py <c> <n>` as before but use a list for the
calendar, not the people.

45. Write a function `polya(dna)` that returns the length of the longest
stretch of As in a dna sequence.

46. Write a program `char_count.py` that prints out the character count of each
character in a file. Invisible characters should be displayed by their ASCII
value rather than the character.

### Sequences

47. Write a function `read_fasta(file)` that reads a FASTA file and returns the
definition line and the sequence.

48. Write a program `gc_analysis.py <fasta> <window>` that computes the average
GC composition and GC skew of a sequence in windows. The two command line
arguments are file name and window size.

49. Write a program `dust.py <fasta> <window> <threshold>` that masks low
complexity DNA sequences, replacing low entropy regions with `N`. Command line
arguments include the file name, window size, and entropy threshold.

50. Write a function `read_fastas(file)` that reads sequences from a
multi-FASTA file, returning one at a time.

## Regex

51. Write a program `queen.py <string>` that solves the NYT Spelling Bee. The
command line argument is the 7 letters, starting with the central letter.

52. Write a program `prosite.py <pattern>` that allows users to search for
prosite patterns in a FASTA file.

## Sets and Dictionaries

53. Write a program `birthday3.py <c> <n>` as before, but use a set.

54. Write a better version of `jaccard.py <file1> <file2>` using sets.

55. Write a better version of `hydropathy(pro)` using a dictionary.

56. Write a better version of `translate(dna)` using a dictionary.

57. Write a function `kmer_count(seq, k)` that breaks up a sequence into kmers
and returns a dictionary of their counts.

58. Write a program `orfeome.py <size>` that estimates the rate of gene-sized
open reading frames per megabase of random sequence. You may assume the
existence of your `translate(dna)` function. The CLI should include the minimum
size of an ORF.

59. Write a program `transmembrane.py <fasta>` that predicts which proteins in
a proteome are embedded in the plasma membrane. Transmembrane proteins are
characterized by having a hydrophobic signal peptide near the N-terminus (first
30 aa) and another hydrophobic region (after 30 aa) to cross the plasma
membrane. Assume the signal peptide is 8 aa long and has average KD >= 2.5 The
transmembrane region is 11 aa long and KD >= 2.0. Neither region may have
prolines. You may assume the existence of your `hydropathy(pro)` function and a
dictionary of hydropathy values.

60. Write a function `read_transfac(file)` that reads a transfac file
describing a position weight matrix, and returns a data structure that indexes
position and nucleotide (e.g. `pwm[pos][nt]`).

------------------------------------------------------------------------------


Practical Programming
=====================

## Patterns

- Use `argparse` for the CLI
- Use `gzip` to read compressed files
- Use `korflab` or your own libraries for common functions
- Create your own test data by sampling real data or making it up
- Perform unit or functional tests
- Write documentation
- Write a tutorial that inculdes minimal test data

## Projects

- Kozak - create the Kozak consensus from the E.coli GenBank file
- mRNA - find the longest ORF in a sequence
- Overlap - find GFF overlaps efficiently
- Needleman-Wunsch - the classic global alignment program
- Smith-Waterman - the classic local alignment problem
- Viterbi - the classic HMM decoder
- Elvish - spoof Elvish with tri-grams of text from the Gutenberg project
- UPGMA - the classic tree-building algorithm
- Boggle - solve a Boggle board quickly
- Unboggle - find the Boggle board with the most words using a GA
- FASTA-SQL - store FASTA files in a SQL database
- GFF-SQL - store GFF files in a SQL database
- C - write some of the 0-60 or Projects in C
