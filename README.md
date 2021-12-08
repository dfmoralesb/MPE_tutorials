# MPE_gene_tree_estimation_tutorial

This repository contains the instructions and data for the ***Tree building and time divergence estimation*** section of the Molecular Phylogenetics and Evolution of Plants course.


## Preparation

### * Requirements (software)


* **IQ-TREE:** IQ-TREE v.2.0.7. Newer versions might be buggy, specially with ultrafast bootstrap annotation. You can find this version of IQ-TREE for Mac OS X, Linux, or Windows can be found on [https://github.com/Cibiv/IQ-TREE/releases](https://github.com/Cibiv/IQ-TREE/releases?page=1).

* **FigTree:** [FigTree](http://tree.bio.ed.ac.uk/software/figtree/) v1.4.4 will be used for tree visualization. Executables for Mac OS X, Linux, and Windows can be found on [https://github.com/rambaut/figtree/releases](https://github.com/rambaut/figtree/releases).

* **ASTRAL** [ASTRAL](https://github.com/smirarab/ASTRAL) v.5.7.1. This program is written in Java and it should be compatible with any OS. It can be found on [https://github.com/smirarab/ASTRAL](https://github.com/smirarab/ASTRAL)

* **BEAST2:** The BEAST2 package v.2.6.6. includes BEAUti, BEAST2, TreeAnnotator, and other tools (e.g., Densitree). The package can be found on the BEAST2 website [https://www.beast2.org](https://www.beast2.org). As all these programs are also written in Java and they all are compatible with any OS. Download the version that comes *with java*.

* **Tracer:** Tracer is also written in Java. The program can be found on [https://github.com/beast-dev/tracer/releases](https://github.com/beast-dev/tracer/releases).


### * Requirements (data)

* All data (e.g, DNA alignments), input files (e.g., XML for BEAST) and output files will be located in the **DATA** folder of this repository.

* **IQ-tree_individual_loci** This folder contains individual loci alignment files (*.phy) from ***ipyrad*** and output files of individual ML gene tree estimation with IQ-TREE.

* **IQ-tree_concatenated** This folder contains the concatenated alignment (*.fa) from all individual loci in folder ***IQ-tree_individual_loci*** and the output files from tree estimation with IQ-TREE.

* **ASTRAL** This folder contains the input file (e.g. all individual gene trees from ***IQ-tree_individual_loci*** in single file) and the output ASTRAL.


### Before you start

* You will need to clone this repository to get all the data on the local computer.

		git clone https://github.com/dfmoralesb/MPE_tutorials.git
		
		
## Phylogenetic inference tutorials

* [Maximum-Likelihood Phylogenetic Inference](tutorials/ML.md)<br>A tutorial on phylogenetic inference with maximum likelihood using IQ-TREE

* [Coalescent-based Species Tree Inference](tutorials/ASTRAL.md)<br>A tutorial on coalescent-based species tree inference with ASTRAL

* [Divergence Time Estimation](tutorials/BEAST.md)<br>A tutorial on divergence time estimation with BEAST2

	
