Database screening
###################

Use cases
=========

The database (DB) screening allows users: 

(1) to estimate the novelty of their gene clusters (a scaffold which does not match similar scaffolds in known databases, is very likely a novel cluster)
(2) the identification of possible post-modifications, which cannot be detected by prediction algorithms yet
(3) the identification of similar clusters (based on the product) 
(4) the matching of custom defined molecules in a genome (using the scaffold upload tool)

Algorithm
=========

.. figure:: img/scaffold_screening.svg
   :scale: 50 %
   :alt: scaffold_screening

The database screening uses a two step approach to identify similar compounds from public DBs.

Fingerprint screening
=====================

First, it screens the selected DBs using molecular fingerprints (FP). For the screening the rdkit implementation
of Morgan FPs (Circular FPs) were chosen (`Morgan Fingerprints <https://www.rdkit.org/docs/GettingStartedInPython.html#fingerprinting-and-molecular-similarity>`_).

In detail a Morgan FB with radius 3 and features is implemented.

The scaffolds of PKS and NRPS often contain multiple times the same building blocks. This property can not 
be accurately represented by bit fingerprints. Multiple identical building block set the same bits (and
bits are only set ones), which lead to similar fingerprints for scaffolds with different amounts of identical fingerprints. 
Therefore, the FPs are implemented as count vectors, which distinguish molecules also based on the amount of present
bits. 

For count vectors the similarity is calculated using dice similarity instead of the well-known Tanimoto coefficient.

When multiple scaffolds are submitted a joint FP is computed for all scaffolds.
This allows SeMPI to match correct scaffolds also of clusters where only fragments could be predicted. 

The FP screening only creates a pre-selection of possible scaffold matches.
This is limited to a certain amount of selections (default: 50), due to the 
long computation time of the follow-up maximum common substructure screening

Maximum Common Substructure Screening
=====================================

Even though the FP screening collects very close matches to the predicted scaffolds, 
some properties cannot be matches accurately with FPs.

For example: The order of building blocks cannot be accurately represented even by count vectors.

Therefore an additional screening is applied to the pre-selected molecules. 

The maximum common substructure (MCS) screening maximizes the MCS for each scaffold fragment with the target 
molecules. 



