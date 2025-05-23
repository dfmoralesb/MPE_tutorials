# MPE tutorials

This repository contains the instructions and tutorials for the **Molecular Phylogenetics and Evolution of Plants course - 2025**.

For tutorial from the **Molecular Phylogenetics and Evolution of Plants course - 2022**, click [here](https://github.com/dfmoralesb/MPE_tutorials_2022/)


## Preparation

#### Workstation account assignment

| Student | USERNAME |
| -------- | ------- |
| Alexander James	Dietrick | mpeuser1 |
| Alexandra	Eisenbeil | mpeuser2 |
| Dikshitha	Siddegowda | mpeuser3 |
| Ece	Cinar | mpeuser4 |
| Jain Mary	Jose | mpeuser5 |
| Jiajun	Ling | mpeuser6 |
| Sushmit	Bhattacharya | mpeuser7 |
| Yusuf	Bozkurt | mpeuser8 |

#### How to login to the workstation

	ssh -p 22110 $USERNAME@
	
The password will be provided at the beginning of the first practicum. 

### Every time you see `$USERNAME` in the example command, you need to replace it with your own

* To avoid having to change the `$USERNAME` for every command, you can set a variable to provide the name of it. ***Do this every time you connect to the workstation***

	For example, for me, Diego, my user name is `mpemaster`
	
		USERNAME=mpemaster


#### Requirements (software): The following software has already been installed in each account.


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


#### You need to install this on each of your working laptops.

* [Aliview](https://ormbunkar.se/aliview/) Use to visualize alignments

* [FigTree](https://github.com/rambaut/figtree/releases) v1.4.4 will be used for tree visualization. 


### * Requirements (data)

All data for analyses and output will be located on the workstation. If not, the tutorial will show you exactly where the data is located.

	/data_tmp/$USERNAME/data
		
		
## Tutorials

By Diego

* [NGS data](tutorials/NGS.md)<br>A tutorial on NGS data and target enrichment data

* [Target enrichment data processing](tutorials/CAPTUS.md)<br>A tutorial on how to process target enrichment data

* [Maximum-Likelihood Phylogenetic Inference](tutorials/ML.md)<br>A tutorial on phylogenetic inference with maximum likelihood using IQ-TREE

* [Coalescent-based Species Tree Inference](tutorials/ASTRAL.md)<br>A tutorial on coalescent-based species tree inference with ASTRAL

* [Phylogenomics](tutorials/ORTHOLOGY.md)<br>A tutorial on the phylogenomics workflow - with a focus on tree-based orthology inference

* [Alternative support values - Conflict analysis](tutorials/CONFLICT.MD)<br>A tutorial on alternative ways to measure node support - with a focus on conflict analyses

* [Identifying Whole Genome Duplication](tutorials/WGD.md)<br>A tutorial on mapping gene duplications using a tree-based approach

By Lizzy

* [Divergence Time Estimation I](https://github.com/joyceem/MPEP_tutorials/blob/main/tutorials/DivergenceTimeEstimation_FossilCalibrations.md)<br>

* [Divergence Time Estimation II](https://github.com/joyceem/MPEP_tutorials/blob/main/tutorials/DivergenceTimeEstimation_BEAST_TargetCapture.md)<br>

* [Ancestral Area Reconstruction](https://github.com/joyceem/MPEP_tutorials/blob/main/tutorials/Ancestral_Area_Reconstruction.md)<br>

* [Ancestral State Reconstruction](https://github.com/joyceem/MPEP_tutorials/blob/main/tutorials/Ancestral_Trait_Reconstruction.md)<br>











