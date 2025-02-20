# MPE tutorials

This repository contains the instructions and tutorias for the **Molecular Phylogenetics and Evolution of Plants course**.


## Preparation

#### Workstation account assignment

| Student | username |
| -------- | ------- |
| Alexander James	Dietrick | mpeuser1 |
| Alexandra	Eisenbeil | mpeuser2 |
| Danila	Blagomirov | mpeuser3 |
| Dikshitha	Siddegowda | mpeuser4 |
| Ece	Cinar | mpeuser5 |
| Helin Meral	Yalcin | mpeuser6 |
| Jain Mary	Jose | mpeuser7 |
| Jiajun	Ling | mpeuser8 |
| Kweku Acheampong	Boakye | mpeuser9 |
| Sushmit	Bhattacharya | mpeuser10 |
| Yusuf	Bozkurt | mpeuser11 |
| Zizheng	Yan | mpeuser12 |

#### How to login to the workstation

	sh -p 22110 [username]@10.153.134.10



#### Requirements (sofware) - The following software has been already installed in each account.


* [fastqc](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)

* [multiqc](https://seqera.io/multiqc/)

* [BBmap](https://sourceforge.net/projects/bbmap/) Includes **Clumpify** (Read deduplication) and **BBduk** (Raw reads adaptor removal and cleaning) 

* [CAPTUS](https://edgardomortiz.github.io/captus.docs/) We will use version 1.1.1 [https://github.com/edgardomortiz/Captus](https://github.com/edgardomortiz/Captus).

* [MAFFT](https://mafft.cbrc.jp/alignment/software/)

* [ClipKIT](https://github.com/JLSteenwyk/ClipKIT)

* [IQ-TREE2](http://www.iqtree.org/)

* [TreeShrink](https://github.com/uym2/TreeShrink) It works with Version 1.3.9 (older versions won't work)

* [ASTRAL and ASTRAL-Pro](https://github.com/chaoszhang/ASTER) Part of the ASTER family of species tree estimator package


#### You need to install this in each of your working laptops.

* [FigTree](https://github.com/rambaut/figtree/releases) v1.4.4 will be used for tree visualization. 

* [Aliview](https://ormbunkar.se/aliview/) Use to visualize alignment




### * Requirements (data)

* All data (e.g, DNA alignments), input files (e.g., XML for BEAST) and output files will be located in the `DATA` folder of this repository.

* **IQ-tree_individual_loci** This folder contains individual loci alignment files (*.phy) from ***ipyrad*** and output files of individual ML gene tree estimation with IQ-TREE.

* **IQ-tree_concatenated** This folder contains the concatenated alignment (*.fa) from all individual loci in folder `IQ-tree_individual_loci` and the output files from tree estimation with IQ-TREE.

* **ASTRAL** This folder contains the input file (e.g. all individual gene trees from `IQ-tree_individual_loci` in single file) and the output ASTRAL.


### Before you start

* You will need to clone this repository to get all the data on the local computer.

		git clone https://github.com/dfmoralesb/MPE_tutorials.git
		
		
## Phylogenetic inference tutorials

* [Maximum-Likelihood Phylogenetic Inference](tutorials/ML.md)<br>A tutorial on phylogenetic inference with maximum likelihood using IQ-TREE

* [Coalescent-based Species Tree Inference](tutorials/ASTRAL.md)<br>A tutorial on coalescent-based species tree inference with ASTRAL

* [Divergence Time Estimation](tutorials/BEAST.md)<br>A tutorial on divergence time estimation with BEAST2

	Here we are going to cover (briefly) only the most relevant aspects of those topic. If you are interested in more comprehensive tutorial you can refer to the great tutorials from [Michael Matschiner](https://evoinformatics.group/) [here](https://github.com/mmatschiner/tutorials). You can always refer to the materials an documentation provided by each software authors.

	
