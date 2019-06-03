Prediction
############

Overview
========

.. figure:: img/prediction.svg
   :scale: 50 %
   :alt: prediction


Protein prediction
==================

The detection of relevant proteins in the genes is performed using profile hidden Markov models (pHMMs) created with HMMER 3.0. This step is common to most prediction tools at present. But as HMMER 3.0 is the state-of-the-art for sensitive sequence homologue detection, there is no reason to reinvent the wheel. Nevertheless, SeMPI uses its own profiles created with in-house sequence databases. The following proteins are detected: 

.. csv-table:: HMM profiles used for domain detection
   :header: "Full name", "Abbrev.", "Remark"
   :widths: 5, 5, 20
   :file: tables/hmm_domains.csv
