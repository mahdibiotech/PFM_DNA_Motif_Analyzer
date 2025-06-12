# PFM_DNA_Motif_Analyzer
A Python tool for analyzing DNA motifs using Position Frequency Matrices (PFM) with multifasta input and motif search.
This project aims to analyze DNA motifs using Position Frequency Matrices (PFM). The goal is to provide a flexible tool that reads DNA sequences in FASTA format, generates a PFM, and uses it to identify motifs in a target sequence.

The program provides insights into conserved regions, consensus sequences, and the positions of motif occurrences in a given DNA sequence. It is designed to be modular and reusable, with clear separation of functionality into three Python files:

multifasta.py: A class for reading and handling DNA sequences from FASTA files.
PFM.py: A class for generating and analyzing Position Frequency Matrices.
main_PFM.py: The main script that integrates the classes and performs the analysis.
------------------------------
1. Features
The program provides the following features:

- Reading multifasta files:
Extract DNA sequences from a FASTA file.

- Building a Position Frequency Matrix (PFM):
Generate a matrix that represents the frequency of bases (A, T, C, G) at each position of the given sequences.

- Motif search:
Identify positions in a target sequence where a motif represented by the PFM occurs.
- Consensus sequence generation:
 Strict consensus sequence: The most frequent base at each position.
 Weak consensus sequence: Displays all possible bases at each position.

- Conserved column detection:
Identify positions where only one base is present across all sequences.

- Searching for motif occurrences:
Identifies all starting positions of motifs represented by the PFM in a given DNA sequence.
---------------------------------------
2. General Principle:

The PFM is calculated based on the input sequences, and it is used to identify occurrences of motifs in the target sequence. Additionally, the program outputs conserved columns, consensus sequences, and other relevant information.

 It takes as input:

- A multifasta file (-sites) containing multiple sequences to generate the PFM.
- A fasta file (-sequence) containing a target sequence to analyze.

Outputs:
The generated PFM from the provided sequences.
Conserved positions in the PFM.
Consensus sequences derived from the PFM.
Positions where the motif defined by the PFM appears in the target sequence.
---------------------------------------------
3. How to Run the Program:
Prerequisites:
Install Python .
Download the required files into the same directory:
main.py
multifasta.py
pfm.py

Command to Run the Program:
Use the following command in a terminal:


python main_PFM.py -sites <path_to_sites.fasta> -sequence <path_to_sequence.fasta>
-----------------------------
4. Example Usage:
Input Files:
- Example File for sites:
 exemple.fasta
>site1
ATGCC
>site2
ATGCT
>site3
ATGCA


- Exemple File for sequence: 
sequence.fasta
>sequence1
GATGCCGATGCTAGTCCGTAAC

----------------------------------
Execution Command:

python main.py -sites sites.fasta -sequence sequence.fasta

Expected Results:  
Position Frequency Matrix (PFM):
3  0  0  0  1
0  3  0  0  1
0  0  0  3  1
0  0  3  0  0

Conserved Sites: [1, 2, 3, 4]

Weak Consensus Sequence: ATGC[ATC]

Positions of PFM occurrences in sequence: [1, 7]

-----------------------------

5. Explanation of Results :

- ****PFM:

Represents the count of each base (A, T, C, G) at each position in the sequences from sites.fasta.

The PFM represents the frequency of each nucleotide (A, T, C, G) at each position across the sequences in sites.fasta. Each row corresponds to a nucleotide (A, T, C, G), and each column represents a position in the sequence. For example:

At position 1, nucleotide A occurs 2 times, and G occurs 3 times.
At position 5, nucleotide A occurs 0 times, while C occurs 2 times.
This matrix is essential for identifying motifs, conserved sites, and consensus sequences.
------------   --------   ----------
-**** Conserved Sites:

Lists the positions where only one base is present across all sequences.
Conserved sites are positions where only one nucleotide is consistently present across all input sequences.

Position 1: G is the only nucleotide.
Position 3: C is the only nucleotide.
These sites indicate regions of the sequences that are invariant and potentially critical for biological functions.

-**** Weak Consensus Sequence:

Displays a sequence with possible bases at each position. Ambiguous positions are shown in brackets.
The weak consensus sequence represents the most flexible motif that can match all sequences in sites.fasta. Each position reflects possible nucleotides:

Position 5: [ACT] means that A, C, or T can occur, indicating variability at this position.


-*****Positions of PFM occurrences in sequence:

These positions indicate the starting points of subsequences in sequence.fasta that match the motif defined by the PFM.

At position 1: The subsequence ATGCC matches the PFM.
At position 7: The subsequence ATGCT matches the PFM.
---------------------
6- Testing and Run Doctests: 
To ensure functionality and validate outputs, run the following command:

python -m doctest -v main_PFM.py multifasta.py PFM.py
-------------------

7. Notes:

a-  Files must be valid FASTA format.
b- All sequences in the -sites file must have the same length.
c- A ValueError is raised if no sequences are found or if the lengths of sequences are inconsistent.
------------------------------
8. Project Layout:

Project
│
├── main_PFM.py: Contains the main function and the motif search logic.
├── multifasta.py:  Implements the Multifasta class for handling multifasta files.
├── pfm.py:  Implements the PFM class for working with Position Frequency Matrices.
├── sites.fasta: A multifasta file with sample motifs.
├── sequence.fasta:  A fasta file with a single target sequence.
└── README.txt: This documentation.
