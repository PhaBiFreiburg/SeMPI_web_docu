
Primer
######

This is the help page of the `SeMPI 2.0 web server <http://sempi.pharmazie.uni-freiburg.de/index>`_.
If you feel there is anything missing or we should include something at this help page please write a mail to:
paul.zierep@pharmazie.uni-freiburg.de 


Introduction
============

SeMPI 2 provides a prediction pipeline for PKS (type I) and NRPS biosynthetic gene cluster (BCG) products. The products are subsequently screened in publicly available natural product databases. The user can modify the product scaffold before submission to the screening algorithm.

.. Detailed information about both cluster types can be found here:

.. https://en.wikipedia.org/wiki/Nonribosomal_peptide
.. https://en.wikipedia.org/wiki/Polyketide_synthase

Help
====

We try to make SeMPI as user-friendly as possible for such a complex pipeline. Therefore, we assign components which are not absolutely self-explanatory with an  question mark. Which upon hovering, displays additional information.

.. figure:: img/help.png
   :scale: 50 %
   :alt: prediction

If you think some components are not clearly explained or need more information, please contact us and we will take care of it.

Version update
==============

The first version of SeMPI used `antiSMASH 3.0 <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4489286/>`_ as gene cluster prediction back end. The main focus was laid on the prediction of 
PKs with a subsequent database screening of the prediction in the StreptomeDB 3.0. Details can be found in the publication
`SeMPI <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5570227/>`_.

SeMPI 2.0 was completed revised and uses its own gene cluster prediction logic. The main improvements are: 

#. Benchmarked and refined profile-HMMs used for domain detection (see :ref:`domain_detection`).
#. Improved gene cluster curration: removal of overlapping domains and combining of duplicated domains (see :ref:`bgc_curration`).
#. Additional prediction of NRPs.
#. PK and NRP substrate specificity prediction using random forest classifiers.
#. NRP substrate prediction based on a classifier trained with more than 2.000 samples.
#. Revised assembly logic for disjointed gene clusters (clusters where the domains are not located on the same gene and in succession).
#. Methylation patterns for PKs and NRPs.
#. Scaffold generation algorithm for NRPS-PKS hybrid clusters.
#. Prediction of the most common postsynthetic modifications. 
#. Improved database screening algorithm using maximum common substructure searches and an addition scoring function to match the postsynthetic modifications.
#. Visual genome browser allowing the dynamically observation of the genome and individual clusters. 
#. A molecular work bench can be used to modify and/or extend the predicted scaffolds before submission to the database screening.
#. Any scaffold can be submitted to the database screening via the `scaffold upload option <http://sempi.pharmazie.uni-freiburg.de/scaffold_upload>`_ even without prior gene cluster prediction (see :ref:`db_screening`).
#. The database screening allows includes 8 publicly available natural product databases (each match includes a link to the original database).
#. The natural product databases also include scaffolds of predicted streptomyces genomes, which enables the reverse search of corresponding gene clusters to a specific secondary metabolite.
#. The natural product database scope can also be extended with custom databases of up to 1.000 scaffolds.
#. The database screening can be used with multiple query scaffolds which will be matched together in the target molecule.

Note
====

Since we are currently in the process of publication of the web server not all underlaying algorithms of the pipeline are explained 
to the full extend. As soon as we have published we will include benchmark results and source code of the server and pipeline. 