Genome input
############

Input form
============

.. figure:: img/screenshots/input_form_01.svg
   :scale: 50 %
   :alt: input


(1) Upload a gene file (DNA) in FASTA or GeneBank format. Drop and drag is also supported.
(2) Its easy to get confused, when multiple files are submitted to the server, therefore the jobs can be commented, which allows simple identification when the jobs are done. An example could be "interesting genome Number 3". This field is optional.
(3) The threshold which defines the maximum distance between functional modules allowing them to be part of the same cluster.
(4) If modules are detected, which lack a functional AT domain, they might be modules using a so called trans-AT (https://pubs.rsc.org/en/content/articlelanding/2016/np/c5np00125k#!divAbstract). In SeMPI 2 their module specificity is set to undefined, but they are still used in the cluster creation process. If the box is unchecked, these modules are set to "not functional".
(5) test

Input format
============

SeMPI can work with genome data in FASTA or GenBank format. 
An example file for both formats can be download from the start page.

Further processing
==================

.. figure:: img/input.svg
   :scale: 50 %
   :alt: input

   If only DNA data is provided, the genes are predicted using prodigal. If the genes are already assigned (GenBank) SeMPI will try to parse the genes and use them for further analysis. SeMPI can parse multiple records per file, it will create one output for each record.