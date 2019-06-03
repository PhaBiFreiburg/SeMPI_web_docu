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
(5) Force the gene prediction algorithm. Independent of the input, the genes will be predicted using prodigal, based on the provided DNA. Otherwise the genes will only be predicted if they cannot be found in the input data. Pre-computed genes need to be assigned in a GeneBank file using the CDS tag (https://www.ncbi.nlm.nih.gov/Sitemap/samplerecord.html#CDSB). As SeMPI 2.0 needs the stand side information of the gene (+ or -) for reasonable cluster predictions, files where the strand side is not assigned will automatically lead to a gene prediction.

.. figure:: img/screenshots/cds_strand.svg
   :alt: input

(6) Force prodigal to use the meta (in new versions also called "Anonymous Mode") option (predicting the genes based on an independent genome training dataset,
https://github.com/hyattpd/Prodigal/wiki/Gene-Prediction-Modes#anonymous-mode). In the normal settings, the meta option is only used, if the provided DNA is too short for accurate self-training.
(7) The screening algorithm uses fingerprints to detect similar compounds in the chosen data bases (DBs) (this gives already close matches). Of those matches the best N. compounds are used for a stricter screening process using most common substructures (MCS). The MCS algorithm can take a while to process, therefore it is reasonable to limit the number of compounds selected for this task (see also :ref:`fp_screen`).


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