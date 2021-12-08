# Phylogenetic Divergence-Time Estimation

A tutorial on phylogenetic divergence-time estimation with with fossils

## Summary

The field of phylogenetic divergence-time estimation has seen tremendous progress over the last two decades, fuelled by increasing availability of molecular data as well as many methodological advances. Some of the most noteworthy advances include the development of Bayesian phylogenetic approaches for divergence-time estimation, the introduction of relaxed-clock models, as well as the implementation of quantitative models of the fossil-sampling process. In particular the latter development promises great improvements in the accuracy of divergence-time estimates as it addresses a major shortcoming of the previously common practice of node dating in which age calibrations were usually specified arbitrarily (and therefore differently by different researchers) due to the absence of quantitative criteria.

## Table of contents

* [Outline](#outline)
* [Dataset](#dataset)
* [Requirements](#requirements)
* [Divergence-time estimation with CladeAge](#cladeage)
* [Divergence-time estimation with the FBD model](#fbd)
* [Interpretation of the inferred timelines](#interpretation)

<a name="outline"></a>



## Table of contents

* [Divergence time estimation with BEAST2](#beast)
* [Running ASTRAL](#running)
* [The ASTRAL Log information](#log)
* [Branch length and support](#support)
* [Reading and visualizing tree files](#figtree)

<a name="beast"></a>
## Divergence time estimation with BEAST2

* Here we will infer ttime-calibrated phylogenies can be inferred with programs of the Bayesian software package [BEAST2](https://www.beast2.org) ([Bouckaert et al. 2014](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1003537)). The settings for the analysis will be done with the program BEAUti, the Bayesian analysis itself is going to be conducted with BEAST2, and a summary tree will be generated with the program TreeAnnotator. These three programs are part of the BEAST2 package. Finally, we explote the use of the program [Tracer](http://beast.community/tracer) ([Rambaut et al. 2018](https://academic.oup.com/sysbio/advance-article/doi/10.1093/sysbio/syy032/4989127)) to assess stationarity and convergence of the Bayesian analysis.


* If you are not familiar  with Bayesian analyses and Markov-Chain Monte Carlo methods in general, you can explore the many resources made available by BEAST2 authors. You can also explore the [BEAST2 website](https://www.beast2.org) and quickly browse through the [glossary of terms related to BEAST2 analyses](https://www.beast2.org/glossary/index.html). The BEAST2 website also provides a [wide range of tutorials and manuals](https://www.beast2.org/tutorials/index.html). Also, you can find comprehensive tutorials on the [Taming the BEAST](https://taming-the-beast.org) website, where you will also find information about the excellent [Taming-the-BEAST workshops](https://taming-the-beast.org/workshops/). 

* We will be using the same data set we used for the concatenated phylogeny with IQ-TREE. All input and out files will be located in the directory `DATA/BEAST`

<a name="beaut"></a>
## Setting the XML file with BEAUti

* The XML [Extensible Markup Language](https://www.w3.org/standards/xml/core) files contains the alignement, priors, and other setting to run the analyses on BEAST.



