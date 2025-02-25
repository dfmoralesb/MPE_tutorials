# MPE tutorials

This repository contains the instructions and tutorias for the **Molecular Phylogenetics and Evolution of Plants course**.


## Preparation

#### Workstation account assignment

| Student | USERNAME |
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
| Diego or Lizzy | mpemaster|

#### How to login to the workstation

	ssh -p 22110 $USERNAME@10.153.134.10
	
The password will be provided at the beginning of the the first practicum. 

### Every time you see `$USERNAME` in the example command you need to replace it with you own

* To avoid having to change the `$USERNAME` for every command you can set a variable to provide the name of it. ***Do this every time you connect to the workstation***

	For example for me Diego my user name is `mpemaster`
	
		USERNAME=mpemaster


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

* [Phyx](https://github.com/FePhyFoFum/phyx)


#### You need to install this in each of your working laptops.

* [Aliview](https://ormbunkar.se/aliview/) Use to visualize alignments

* [FigTree](https://github.com/rambaut/figtree/releases) v1.4.4 will be used for tree visualization. 


### * Requirements (data)

All data for analyses and output will be located in

	/data_tmp/USERNAME/data
		
		
## Tutorials

* [NGS data](tutorials/NGS.md)<br>A tutorial on NGS data and target enrichment data

* [Target enrichment data processing](tutorials/CAPTUS.md)<br>A tutorial on how to process target enrichment data

* [Maximum-Likelihood Phylogenetic Inference](tutorials/ML.md)<br>A tutorial on phylogenetic inference with maximum likelihood using IQ-TREE

* [Coalescent-based Species Tree Inference](tutorials/ASTRAL.md)<br>A tutorial on coalescent-based species tree inference with ASTRAL

* [Phylogenomics](tutorials/ORTHOLOGY.md)<br>A tutorial on the phylogenomics workflow - with a focus on tree-based orthology inference

* [Alternative support values - Conflict analysis](tutorials/CONFLICT.MD)<br>A tutorial on alternative way to measure node support - wit a focus on conflict analyses

	Here we are going to cover (briefly) only the most relevant aspects of those topic. If you are interested in more comprehensive tutorials you can refer to the great tutorials from [Michael Matschiner](https://evoinformatics.group/) [here](https://github.com/mmatschiner/tutorials). You can always refer to the materials an documentation provided by each software authors.


