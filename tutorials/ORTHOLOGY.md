## Table of contents

* [Phylogenomics workflow](#phylo)
* [Loci assembly](#assembly)
* [Running ASTRAL](#running)
* [The ASTRAL Log information](#log)
* [Branch length and support](#support)
* [Reading and visualizing tree files](#figtree)

#### How to login to the workstation

	ssh -p 22110 [username]@10.153.134.10


### Every time you see `[username]` in the example command you need to replace it with you own [username](https://github.com/dfmoralesb/MPE_tutorials/blob/main/README.md)<br>

<a name="phylo"></a>
## Phylogenomics workflow with a focus on tree-based orthology inference

* For more detail of the phylogenomics workflow that we will follow see [here](https://doi.org/10.1093/sysbio/syab032)

	But in general consists of the following steps.
	
	<p align="center"><img src="images/wf.png" alt="wf" width="400"></p>


<a name="assembly"></a>
## Loci assembly, Paralog assembly, and alignment

* We previously learn how to use Captus to assembly, extract and aligned the loci.

	We have already seen the Captus reports for all those steps for the full 30-taxa data set.
	
	I just want to point point out to the last command for Captus (align)

		captus align -e 03_extraction/ -m NUC -f GE --max_paralogs 5 --min_samples 4 --align_method mafft_auto --outgroup RUTA_Citrus_hystrix,RUTA_Melicope_ternata,RUTA_Ruta_graveolens --filter_method none --clipkit_method gappy --clipkit_gaps 0.9 --threads 90 --concurrent 30	

	Here, I want you to point attention to the flag `--max_paralogs 5` meaning that the loci that we will work have up to 5 copies per sample. This is the part referred as `Paralog assesment` in the workflow. Other assembly pipelines required additional steps identify and collect gene copies. With Captus is as simple as using one flag to collect them.
	
	
	

