Genome input
############

Input form
============

.. figure:: img/screenshots/input_form_01.svg
   :scale: 50 %
   :alt: input

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