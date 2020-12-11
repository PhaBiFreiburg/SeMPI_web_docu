Prediction
############

This is the work flow of the gene cluster detection and scaffold pipeline.

Gene prediction
===============

If only DNA data is provided, the genes are
predicted using `Prodigal <https://github.com/hyattpd/Prodigal>`_. 
If the genes are already assigned, SeMPI can try to parse the genes and
use them for further analysis.

.. _domain_detection:

Domain detection
================

The detection of relevant domains in the predicted proteins is performed using profile hidden Markov models (profile-HMMs) 
created with HMMER 3.0. The detected domains are shown in :numref:`phmms`. Since the profile-HMMs are derived and modified from the MIBiG 2 database, the nomenclature is mainly based on the antiSMAHS definition as described in their `documentation <https://docs.antismash.secondarymetabolites.org/modules/nrps_pks_domains/>`_.

.. _phmms:
.. csv-table:: HMM profiles used for domain detection. The F1-scores and thresholds are based on the detection performance of the profile-HMMs on the `MIBiG 2.0 database <https://mibig.secondarymetabolites.org/>`_.
   :header: "Domain", "Full name", "F1-score", "HMM detection threshold (domT)"
   :widths: 5, 10, 5, 5
   :file: tables/hmm_domains.csv

.. _bgc_curration:

Gene cluster curation
=====================

After the protein detection the genome is converted into a DataFrame `pandas <https://pandas.pydata.org/>`_, which simplifies the subsequent operations. Additional, pandas allows to apply vectorized functions, which speeds up the prediction pipeline. A mysql dump of the DataFrames is provided with the final output.

The DataFrame is curated and modified in order to prepare the BGC module detection (see Example :numref:`df-processing`). 

(a) Close genes (the threshold can be set in the options of the :ref:`upload_form`) which encode proteins on the same strand are combined into blocks. A detailed observation of the MIBiG annotated NRP and PK clusters showed, that for this condition the co-linearity principle applies for the very most cases. 
(b) The domains are ordered based on the occurrence in the genome (id), but for module assignment it is more useful to order the domains based on the occurrence in the block, therefore an additional index is assigned based on the block order (Corr. id). 
(c) In very rare cases the detected protein domains overlap. This can be the case especially for very short sequences (for example the ACP domain). If the domains overlap to more then 20% the domain with the lower bitscore (see `HMMER <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3125773/>`_) is removed. 
(d) Sometimes the HMM algorithm detects two domains in succession instead of one domain, these domains are automatically joined to one domain.


.. _df-processing:
.. figure:: img/df_processing.svg
   :scale: 50 %
   :alt: prediction

   Curation steps: (a) Block generation, (b) Domain reordering, (c) Domain overlap removal, (d) Domain duplication joining.

.. _mod_detect:

Module detection
================

SeMPI v2 detects functional PKS and NRPS modules based on a in-depth analysis
of known gene clusters stored in the MIBiG 2.0.
The modules can be be observed either in the tabular 
representation (see Example :numref:`mods1`) of the domains of a gene cluster or 
in the interactive cluster browser (see Example :numref:`mods2`). 

.. _mods1:
.. figure:: img/screenshots/mods_01.png
   :alt: mods1

   Tabular domain representation of a gene cluster with modules highlighted in red. 

.. _mods2:
.. figure:: img/screenshots/mods_02.png
   :alt: mods2

   Cluster browser representation of a gene cluster with modules highlighted in red. 


Assembly logic for disjointed gene clusters 
===========================================

If the domains are not organized in a single consecutive block an module ordering algorithm is applied. 
In most cases (<= 3 blocks) the assignment of starting modules to the beginning and terminal modules to the end of an gene cluster
is sufficient for a correct module order.
For gene clusters with more than 3 blocks the modules are ordered based on comparison of the 
gene cluster assembly with the set-up of more than 250 reference gene clusters where the module order is known.

Postsynthetic modifications 
===========================

In order to detect postsynthetic modifications additional `Pfam domains <http://pfam.xfam.org/>`_ are detected in proximity of the gene cluster.
The Pfam domains are correlated to specific postsynthetic modifications as shown in :numref:`pfams`.

.. _pfams:
.. csv-table:: Detected Pfam domains correlated to common postsynthetic modifications.
   :header-rows: 1
   :widths: 5, 5, 10, 5
   :file: tables/summary_pfam_post_mod.csv
   :delim: U+003B

Based on the detected domains the postsynthetic modifications are predicted using regression models.
The predicted numbers of postsynthetic modifications are shown together with the predicted scaffold as shown in :numref:`psm`.

.. _psm:
.. figure:: img/screenshots/psms_example.jpg
   :scale: 90 %
   :alt: psm example

   Example of an PK scaffold prediction with indicated halogen (Cl) postsynthetic modification.

Scaffold generation
===================

The scaffolds are generated by joining of each building block of a gene cluster. 
If the modules of a cluster cannot be joined multiple blocks are generated (see Example :numref:`scaff1`). The database screening queries all blocks in the target   
molecules (see Example :numref:`scaff2`).  
The example is taken from `BGC0000317 <http://sempi.pharmazie.uni-freiburg.de/results/21839>`_.
The multiple blocks scaffoled scoring algorithm is further described in :ref:`mcs_rank`.

.. _scaff1:
.. figure:: img/screenshots/scaff1.jpg
   :alt: mods1

   Two blocks predicted for one cluster. 

.. _scaff2:
.. figure:: img/screenshots/scaff2.jpg
   :alt: mods2

   Both blocks are screened in each of the target compounds. 
