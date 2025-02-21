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

	ssh -p 22110 [username]@10.153.134.10
	
The password will be provided at the beginning of the the first practicum. 



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

All data for analyses and output will be located in

	/data_tmp/[username]/data
		
		
## Tutorials

* [NGS data](tutorials/NGS.md)<br>A tutorial on NGS data and target enrichment data

* [Target enrichment data processing](tutorials/CAPTUS.md)<br>A tutorial on how to process target enrichment data

* [Maximum-Likelihood Phylogenetic Inference](tutorials/ML.md)<br>A tutorial on phylogenetic inference with maximum likelihood using IQ-TREE

* [Coalescent-based Species Tree Inference](tutorials/ASTRAL.md)<br>A tutorial on coalescent-based species tree inference with ASTRAL

* [Divergence Time Estimation](tutorials/BEAST.md)<br>A tutorial on divergence time estimation with BEAST2

	Here we are going to cover (briefly) only the most relevant aspects of those topic. If you are interested in more comprehensive tutorial you can refer to the great tutorials from [Michael Matschiner](https://evoinformatics.group/) [here](https://github.com/mmatschiner/tutorials). You can always refer to the materials an documentation provided by each software authors.

	
