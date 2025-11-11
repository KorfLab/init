A to Z Programming
==================

WARNING: THIS IS VOLATILE AND UNFINISHED

This is a collection of 26 bioinformatics-themed coding exercises that will
improve your programming skill. Some problems require data files, which you
will find in the `data` directory. You should not import any external
libraries: this is designed for learning, not productivity.

- [acgt](#acgt)
- [bits](#bits)
- [celsius](#celsius)
- [dna_tm](#dna_tm)
- [euler](#euler)
- [fasta_file](#fasta_file)
- [gregory](#gregory)
- [hydropathy](#hydropathy)
- [information](#information)
- [jaccard](#jaccard)
- [kmer_count](#kmer_count)
- [low_entropy](#low_entropy)
- [mc_birthday](#mc_birthday)
- [n50](#n50)
- [orfs](#orfs)
- [prosite](#prosite)
- [quorum](#quorum)
- [ribosome](#ribosome)
- [smith](#smith)
- [thalassian](#thalassian)
- [upgma](#upgma)
- [viterbi](#viterbi)
- [word_search](#word_search)
- [xref_gff](#xref_gff)
- [yaml_gff](#yaml_gff)
- [zero](#zero)


## acgt ##

Write a program that randomly prints out a single letter of DNA. In most
eukarytotic genomes, you are more likely to see an A or T than C or G, so make
the program do that also. In the human genome, about 60% is A/T and 40% is C/G.

Example of command line and output:

```
$ python3 acgt.py
A
$ python3 acgt.py
T
```

## bits ##

Write a program that prompts the user for a number. The number is then
represented in log2. Note that numbers that are 0 or less will produce errors.

Example of command line and output:

```
$ python3 bits.py
Please enter a number to convert: 4
2.0
```

## celsius ##

Write a program that converts from Celsius to Farenheit and vice-versa. The
input should be in the form of "37C or "98.6F". If the input is "37C" the
output should be "98.6F". After providing an answer, the program should
continue accepting input until the user enters a blank line.

Example of command line and input/output:

```
$ python3 celsius.py
What temperature to convert (e.g. 37C or 98.6F): 37C
37.0C is 98.6F
What temperature to convert (e.g. 37C or 98.6F): 98.6F
98.6F is 37.0C
What temperature to convert (e.g. 37C or 98.6F):
```

## dna_tm ##

Write a program that allows users to compute the melting temperature (Tm) of an
oligonucleotide (short DNA sequence) by typing (or copy-paste). The program
should quit if the input is empty and terminate with an error message if the
sequence contains letters other than A, C, G, or T. There are 2 formulas for
Tm, which depend on the length of the sequence. Your code must define a
function `tm()` that takes a sequence as an argument and returns the Tm. Here
are the 2 equations:

- 13 nt or less: 2*A + 2*T + C*4 + G*4
- 14 nt or more: 64.9 + 41 * (C + G -16.4) / (A + C + G + T)

Example of command line and input/output

```
$ python3 dna_tm.py
Oligo sequence: TAATACGACTCACTATAGGG
The Tm of TAATACGACTCACTATAGGG is 47.680C
```

## euler ##

Write a program that estimates Euler's number, e (2.71828...). This is the sum
of 1/n! ad infinitum. Write your own factorial function rather than using
`math.factorial()`. Print the value of e with each iteration of the loop.
Terminate the loop when the value of e no longer changes (runs out of
precision and repeats itself).

Example command line and output:

```
$ python3 euler.py
1.0
2.0
2.5
2.6666666666666665
2.708333333333333
2.7166666666666663
2.7180555555555554
2.7182539682539684
2.71827876984127
2.7182815255731922
2.7182818011463845
2.718281826198493
2.7182818282861687
2.7182818284467594
2.71828182845823
2.718281828458995
2.718281828459043
2.7182818284590455
```

## fasta_file ##

Write a program the creates a random fasta file. This program takes a command
line argument, which is the length of the sequence.

```
$ python3 fasta_file.py 40
>random_sequence
AGATACGATATACCAGATATATCATATTACGAGAAAATAT
```

## gregory ##

Write a program that esimates Pi (3.1415...) using 3 different methods.

1. Gregory-Leibniz series
2. Nilakantha series
3. Simulation by throwing random darts

The Gregory-Leibniz series is a simple way to estimate Pi. It alternates adding
and subtracting numbers, eventually converging to Pi/4. Use a loop that
terminates after some number of iterations (e.g. 1000).

Pi/4 = 1/1 - 1/3 + 1/5 - 1/7 + 1/9 ...

The Nilakantha series converges faster and is only slightly more complex to
calculate. Terminate this loop when the estimate of Pi is within 1e-6 of the
actual value (you must pretend you don't know the value of Pi).

Pi = 3 + 4/(2*3*4) - 4/(4*5*6) + 4/(6*7*8) - 4/(8*9*10) ...

A particularly poor (but fun) way to calculate Pi is to simulate throwing darts
with random x, y values in the range from 0 to 1 (e.g. a dart might land at
x=0.35, y=0.84). The ratio of darts that lie inside the circle y = x**2
compared to the total darts eventually converges to Pi/4. It's up to you how
you want to terminate this part.

https://en.wikipedia.org/wiki/Pi

```
$ python3 gregory.py  | less
Gregory odd-even: 3.140592653839794
Gregory flip-flop: 3.140592653839794
Nilakantha definite: 3.141839618929402
Nilakantha indefinite: 3.1666666666666665
Nilakantha indefinite: 3.1333333333333333
Nilakantha indefinite: 3.145238095238095
Nilakantha indefinite: 3.1396825396825396
Nilakantha indefinite: 3.1427128427128426
Nilakantha indefinite: 3.1408813408813407
Nilakantha indefinite: 3.142071817071817
Nilakantha indefinite: 3.1412548236077646
Infinite: 2.6666666666666665
Infinite: 3.0
Infinite: 3.2
Infinite: 3.3333333333333335
Infinite: 3.4285714285714284
Infinite: 3.0
Infinite: 3.111111111111111
Infinite: 3.2
Infinite: 3.272727272727273
Infinite: 3.3333333333333335
```

## hydropathy ##

Write a program that calculates the hydropathy of a sequence given as a command
line argument. Use the Kyte-Doolittle hydropathy scale.

```
$ python/hydropathy.py  MVSLPTVLQRVILN
Average hydropathy: 1.129
```

https://en.wikipedia.org/wiki/Hydrophilicity_plot
https://en.wikipedia.org/wiki/Hydrophobicity_scales


## information ##

Write a program that calculates the information content (entropy) of a
frequency distribution whose values are given on the command line.

- The values from the command line must be converted to a list of floats
- The container must sum very close to 1.0 or produce an error message
- The program must define a function `entropy()` that accepts the container
- The program must return the result in log2

```
$ python3 information.py 0.4 0.3 0.2 0.1
1.8464393446710154
```


## jaccard ##

Given 2 files, each containing a list of gene names, determine the Jaccard
Index between the two. The Jaccard Index is defined as the intersection divided
by the union. For this problem, you must use lists (arrays, vectors) not
organized data structures (sets, hashes, maps, dictionaries, trees).

You will find files of gene names ...

https://en.wikipedia.org/wiki/Jaccard_index

-----

This program introduces:

- File input
- Searching a list

This program reinforces the use lists in general and searching for specific
elements in particular. Most built-in search mechanisms are linear, however,
the more advanced progammers may choose to sort their list and then use binary
search. Of course, there are more efficient ways to solve the problem using
more organized data structures, but these are not introduced until...

## kmer_count ##

Write a program that counts the kmers in a fasta file

## low_entropy ##

Commmand line parameters for file, window size, threshold

-----

Introduces:

- Windowing algorithm
- FASTA file reading (single record only)
- Converting a string into a list (some languages)


Forward reference to rloop and shannon and argparse?

## mc_birthday ##

Birthday paradox...

## n50 ##

Various stats including n50

## orfs ##

Translate sequences

## prosite ##

Use dictionaries

## quorum ##

Find the best concensus sequence and IUPAC representation

## ribosome ##

Create Kozak PWM from a GenBank file

## smith ##

Smith-Waterman

## thalassian ##

Create Elvish from text

## upgma ##

Classic clustering algorithm

## viterbi ##

Viterbi

## word_search ##

Find words in a grid of letters (like Boggle)

## xref_gff ##

Find overlapping features in 2 gff files

## yaml_gff ##

Convert GFF to YAML preserving parent-child relationships in genes. Infer
introns and UTRs.

## zero ##

Perform a ground-zero re-write of every program. If you've already done that,
do it in a different language.
