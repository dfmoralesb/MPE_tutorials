## Table of contents

* [Phylogenomics workflow](#phylo)
* [Loci assembly, Paralog assembly, and alignment](#assembly)
* [Tip Masking](#masking)
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
	
* The final output of Captus for all 30 species and 353 genes is located in the directory `/data_tmp/mpemaster/output/03_captus/04_alignments/03_trimmed/04_unfiltered/01_coding_NUC/03_genes`

		cd /data_tmp/mpemaster/output/03_captus/04_alignments/03_trimmed/04_unfiltered/01_coding_NUC/03_genes
		
	You can see all files with the command `ls`
	
		4471.fna  5034.fna  5280.fna  5426.fna  5594.fna  5791.fna  5913.fna  5981.fna  6119.fna  6298.fna  6412.fna  6506.fna  6639.fna  6797.fna  6958.fna  7241.fna
		4527.fna  5038.fna  5296.fna  5427.fna  5596.fna  5802.fna  5918.fna  5990.fna  6128.fna  6299.fna  6420.fna  6507.fna  6641.fna  6825.fna  6961.fna  7273.fna
		4691.fna  5064.fna  5299.fna  5428.fna  5599.fna  5815.fna  5919.fna  6000.fna  6130.fna  6303.fna  6432.fna  6526.fna  6649.fna  6848.fna  6962.fna  ...

	You can count how many loci were able to collect by counting the number of fasta files.
	
	
		ls *.fna | wc -l
		
	You will see that we have `348` files.
	
* We can explore one of the fasta files to see if there are samples that have multiple copies. For example:


		grep ">" 4471.fna | sort
	
	Then you should see
	
		>MELI_Aglaia_spectabilis__00 [query=TJLC-4471] [hit=00] [wscore=0.737] [cover=99.55] [ident=87.00] [score=0.737] [length=2992]
		>MELI_Aglaia_spectabilis__01 [query=TJLC-4471] [hit=01] [wscore=0.386] [cover=83.04] [ident=77.96] [score=0.464] [length=1896]
		>MELI_Aglaia_spectabilis__02 [query=TJLC-4471] [hit=02] [wscore=0.366] [cover=72.77] [ident=85.28] [score=0.513] [length=2420] [frameshifts=1827,1828]
		>MELI_Aphanamixis_polystachya__00 [query=TJLC-4471] [hit=00] [wscore=0.792] [cover=99.11] [ident=90.09] [score=0.795] [length=2453]
		>MELI_Aphanamixis_polystachya__01 [query=TJLC-4471] [hit=01] [wscore=0.387] [cover=83.48] [ident=77.54] [score=0.460] [length=2144]
		>MELI_Azadirachta_indica [query=TJLC-4471] [hit=00] [wscore=0.843] [cover=99.55] [ident=92.38] [score=0.844] [length=3199]
		>MELI_Cabralea_canjerana__00 [query=QUTB-4471] [hit=00] [wscore=0.762] [cover=99.53] [ident=88.26] [score=0.762] [length=3050]
		>MELI_Cabralea_canjerana__01 [query=QUTB-4471] [hit=01] [wscore=0.378] [cover=76.64] [ident=82.93] [score=0.505] [length=2474] [frameshifts=1073,1074]
		>MELI_Cabralea_canjerana__02 [query=QUTB-4471] [hit=02] [wscore=0.286] [cover=63.55] [ident=85.29] [score=0.449] [length=1283]
		>MELI_Chisocheton_longistipitatus__00 [query=TJLC-4471] [hit=00] [wscore=0.780] [cover=99.55] [ident=89.24] [score=0.781] [length=2784]
		>MELI_Chisocheton_longistipitatus__01 [query=TJLC-4471] [hit=01] [wscore=0.752] [cover=99.55] [ident=87.89] [score=0.754] [length=2962]
		>MELI_Chukrasia_tabularis [query=AJFN-4471] [hit=00] [wscore=0.674] [cover=94.54] [ident=85.78] [score=0.676] [length=2064]
		>MELI_Dysoxylum_alliaceum [query=TJLC-4471] [hit=00] [wscore=0.695] [cover=84.82] [ident=91.05] [score=0.696] [length=1828]
		>MELI_Guarea_pubescens__00 [query=TJLC-4471] [hit=00] [wscore=0.766] [cover=100.00] [ident=88.39] [score=0.768] [length=2999]
		>MELI_Guarea_pubescens__01 [query=TJLC-4471] [hit=01] [wscore=0.662] [cover=99.55] [ident=84.30] [score=0.683] [length=3221] [frameshifts=371]
		>MELI_Guarea_pubescens__02 [query=TJLC-4471] [hit=02] [wscore=0.305] [cover=68.75] [ident=83.12] [score=0.455] [length=1394] [frameshifts=726,727]
		>MELI_Heckeldora_staudtii__00 [query=TJLC-4471] [hit=00] [wscore=0.794] [cover=100.00] [ident=89.73] [score=0.795] [length=3057]
		>MELI_Heckeldora_staudtii__01 [query=TJLC-4471] [hit=01] [wscore=0.288] [cover=68.30] [ident=81.70] [score=0.433] [length=1449] [frameshifts=615]
		>MELI_Lovoa_sywnnertonii__00 [query=TJLC-4471] [hit=00] [wscore=0.812] [cover=100.00] [ident=90.62] [score=0.812] [length=2784]
		>MELI_Lovoa_sywnnertonii__01 [query=TJLC-4471] [hit=01] [wscore=0.461] [cover=83.48] [ident=83.96] [score=0.567] [length=2351] [frameshifts=890]
		>MELI_Melia_azedarach [query=QUTB-4471] [hit=00] [wscore=0.815] [cover=95.79] [ident=92.68] [score=0.818] [length=2224]
		>MELI_Neoguarea_glomerulata__00 [query=TJLC-4471] [hit=00] [wscore=0.633] [cover=83.04] [ident=88.17] [score=0.634] [length=2132]
		>MELI_Neoguarea_glomerulata__01 [query=TJLC-4471] [hit=01] [wscore=0.443] [cover=68.75] [ident=88.96] [score=0.536] [length=1943]
		>MELI_Owenia_reticulata [query=VUSY-4471] [hit=00] [wscore=0.764] [cover=93.84] [ident=90.73] [score=0.764] [length=3302]
		>MELI_Quivisianthe_papinae [query=VFFP-4471] [hit=00] [wscore=0.755] [cover=88.25] [ident=92.81] [score=0.756] [length=3792]
		>MELI_Schmardaea_microphylla [query=VUSY-4471] [hit=00] [wscore=0.754] [cover=93.84] [ident=90.35] [score=0.757] [length=3063]
		>MELI_Swietenia_macrophylla [query=TJLC-4471] [hit=00] [wscore=0.790] [cover=99.55] [ident=89.69] [score=0.790] [length=2585]
		>MELI_Toona_ciliata__00 [query=TJLC-4471] [hit=00] [wscore=0.848] [cover=100.00] [ident=92.41] [score=0.848] [length=2823]
		>MELI_Toona_ciliata__01 [query=TJLC-4471] [hit=01] [wscore=0.840] [cover=99.55] [ident=92.38] [score=0.844] [length=2579]
		>MELI_Trichilia_hirta [query=QUTB-4471] [hit=00] [wscore=0.779] [cover=95.79] [ident=90.73] [score=0.780] [length=2346]
		>MELI_Turraea_virens [query=TJLC-4471] [hit=00] [wscore=0.790] [cover=99.55] [ident=89.69] [score=0.790] [length=2795]
		>MELI_Vavaea_amicorum__00 [query=TJLC-4471] [hit=00] [wscore=0.772] [cover=99.55] [ident=88.79] [score=0.772] [length=3097]
		>MELI_Vavaea_amicorum__01 [query=TJLC-4471] [hit=01] [wscore=0.515] [cover=95.54] [ident=80.37] [score=0.580] [length=1944] [frameshifts=54,1592,1877,1878]
		>RUTA_Citrus_hystrix [query=TJLC-4471] [hit=00] [wscore=0.772] [cover=99.55] [ident=88.79] [score=0.772] [length=3359]
		>RUTA_Melicope_ternata [query=TJLC-4471] [hit=00] [wscore=0.647] [cover=83.48] [ident=88.77] [score=0.647] [length=2166]
		>RUTA_Ruta_graveolens__00 [query=VFFP-4471] [hit=00] [wscore=0.786] [cover=99.68] [ident=89.49] [score=0.787] [length=3298]
		>RUTA_Ruta_graveolens__01 [query=VFFP-4471] [hit=01] [wscore=0.779] [cover=99.68] [ident=89.17] [score=0.781] [length=3048]

<a name="homolog"></a>
## Homolog tree inference

* Now we are going to infer ML homolog trees. Here we refer to homolog trees the gene trees that have all gene copies.

* To use the scripts for the phylogenomics workflow an "@" symbol needs to be added in the fasta headers to identify paralogs of the same sample.

	Meaning that instead of having the long fasta headers you see above, we want something that looks like this:
	
		>MELI_Aglaia_spectabilis@pg_00
		>MELI_Aglaia_spectabilis@pg_01
		>MELI_Aglaia_spectabilis@pg_02
		>MELI_Aphanamixis_polystachya@pg_00
		>MELI_Aphanamixis_polystachya@pg_01
		>MELI_Azadirachta_indica@pg_uq
		>MELI_Cabralea_canjerana@pg_00
		>MELI_Cabralea_canjerana@pg_01
		>MELI_Cabralea_canjerana@pg_02
		>MELI_Chisocheton_longistipitatus@pg_00
		>MELI_Chisocheton_longistipitatus@pg_01
		>MELI_Chukrasia_tabularis@pg_uq
		>MELI_Dysoxylum_alliaceum@pg_uq
		>MELI_Guarea_pubescens@pg_00
		>MELI_Guarea_pubescens@pg_01
		>MELI_Guarea_pubescens@pg_02
		>MELI_Heckeldora_staudtii@pg_00
		>MELI_Heckeldora_staudtii@pg_01
		>MELI_Lovoa_sywnnertonii@pg_00
		>MELI_Lovoa_sywnnertonii@pg_01
		>MELI_Melia_azedarach@pg_uq
		>MELI_Neoguarea_glomerulata@pg_00
		>MELI_Neoguarea_glomerulata@pg_01
		>MELI_Owenia_reticulata@pg_uq
		>MELI_Quivisianthe_papinae@pg_uq
		>MELI_Schmardaea_microphylla@pg_uq
		>MELI_Swietenia_macrophylla@pg_uq
		>MELI_Toona_ciliata@pg_00
		>MELI_Toona_ciliata@pg_01
		>MELI_Trichilia_hirta@pg_uq
		>MELI_Turraea_virens@pg_uq
		>MELI_Vavaea_amicorum@pg_00
		>MELI_Vavaea_amicorum@pg_01
		>RUTA_Citrus_hystrix@pg_uq
		>RUTA_Melicope_ternata@pg_uq
		>RUTA_Ruta_graveolens@pg_00
		>RUTA_Ruta_graveolens@pg_01

* First we going to for make a copy of the alignments to a new directory so we can reformat them

		cp /data_tmp/mpemaster/output/03_captus/04_alignments/03_trimmed/04_unfiltered/01_coding_NUC/03_genes/*.fna /data_tmp/mpemaster/data/07_phylogenomic_analyses/01_clean_alignments
		
	
* Now move to the new directory where the copy of the fasta files are located and use `ls` see make sure they are there
	
	
		cd /data_tmp/mpemaster/data/07_phylogenomic_analyses/01_clean_alignments
		
		ls
		
* Now we can format them using the the following loop
	
	
		for i in $(ls *.fna); do
		sed -i -E 's/(>.+)(__)([[:digit:]]+)( .+)/\1@pg_\3/' $i
		sed -i -E 's/(>.+)( \[query=.+)/\1@pg_uq/' $i
		done
		
	After is done you can verify if the format is the correct
	
		grep ">" 4471.fna
		
* Now all these alignment are ready for ML tree inference

	Because of time restriction we are not going to run all `348` tree. I run this previously. As we learn before I use IQ-Tree for this. I run the following command for each tree. This is just so you know what I did.
	
	
		iqtree -m MFP -s [alignment] -T 4 --seqtype DNA
	

	
	The output of IQ-tree can be found here `/data_tmp/mpemaster/output/04_analyses/00_iqtree`
	
	
		cd /data_tmp/mpemaster/output/04_analyses/00_iqtree
		
		ls
		
	You can see all the `*.treefile` files
	
	
* Unfortunately, IQ-tree does now like the `@` symbol in the taxa label and replace it with an `underscore` so we need to put back the `@` back to each tree.
	
	Check one tree to see this.
	
		(RUTA_Citrus_hystrix_pg_uq:0.0967470193,(RUTA_Melicope_ternata_pg_uq:0.1621729005,(((((((((((MELI_Aglaia_spectabilis_pg_00:0.0379882798,MELI_Cabralea_canjerana_pg_00:0.0199533071):0.0085782116,(MELI_Chisocheton_longistipitatus_pg_00:0.0379882310,MELI_Aphanamixis_polystachya_pg_00:0.0494920662):0.0092253339):0.0021483280,MELI_Dysoxylum_alliaceum_pg_uq:0.0471504315):0.0015887986,MELI_Neoguarea_glomerulata_pg_01:0.0547080994):0.0008844444,MELI_Guarea_pubescens_pg_00:0.0533609950):0.0063054953,(((MELI_Aglaia_spectabilis_pg_02:0.0388463469,MELI_Cabralea_canjerana_pg_01:0.0216316868):0.0101132600,(MELI_Chisocheton_longistipitatus_pg_01:0.0387180305,((MELI_Heckeldora_staudtii_pg_00:0.0335110710,MELI_Neoguarea_glomerulata_pg_00:0.0618294687):0.0012785897,MELI_Guarea_pubescens_pg_02:0.0446490573):0.0018537144):0.0008490844):0.0027375406,MELI_Vavaea_amicorum_pg_00:0.0681955907):0.0029342096):0.0119221091,(MELI_Trichilia_hirta_pg_uq:0.0535061946,MELI_Turraea_virens_pg_uq:0.0851368654):0.0201718173):0.0016617099,((((MELI_Aglaia_spectabilis_pg_01:0.0519234782,MELI_Aphanamixis_polystachya_pg_01:0.0540052513):0.0009267065,MELI_Cabralea_canjerana_pg_02:0.0149007675):0.0150915790,(MELI_Guarea_pubescens_pg_01:0.0394354788,MELI_Heckeldora_staudtii_pg_01:0.0487069879):0.0065479564):0.0014578384,MELI_Vavaea_amicorum_pg_01:0.0835631202):0.0168885015):0.0115562485,MELI_Quivisianthe_papinae_pg_uq:0.0811917761):0.0341719786,((MELI_Azadirachta_indica_pg_uq:0.0004945456,MELI_Melia_azedarach_pg_uq:0.0015084365):0.0294961855,MELI_Owenia_reticulata_pg_uq:0.0294422745):0.0650087238):0.0047714922,((MELI_Swietenia_macrophylla_pg_uq:0.0692218925,(MELI_Toona_ciliata_pg_00:0.0225271377,MELI_Lovoa_sywnnertonii_pg_00:0.0531688410):0.0110747809):0.0144563047,((MELI_Toona_ciliata_pg_01:0.0268624674,MELI_Lovoa_sywnnertonii_pg_01:0.0711210879):0.0140801051,(MELI_Schmardaea_microphylla_pg_uq:0.0915458593,MELI_Chukrasia_tabularis_pg_uq:0.0562293914):0.0059356522):0.0049522269):0.0154278084):0.1260643977):0.0171517151,(RUTA_Ruta_graveolens_pg_00:0.0160212743,RUTA_Ruta_graveolens_pg_01:0.0230618982):0.1840426818);
	
	
	
* To reformat the tree files we first are going to make a copy of all the `*.treefile` in new directory
	
	
		cp /data_tmp/mpemaster/output/04_analyses/00_iqtree/*.treefile /data_tmp/mpemaster/data/07_phylogenomic_analyses/02_raw_homolog_trees
		
		
	Make a list to see the files
	
		cd /data_tmp/mpemaster/data/07_phylogenomic_analyses/02_raw_homolog_trees
	
		ls
		
* Now tha we have the tree files in the directory we can format them with the following loop
	
	
		for i in $(ls *.treefile)
		do
		perl -p -i -e "s/_pg/\@pg/g" $i
		done

	You can check one file to verify that the species contain the `@` symbol
	
	 	cat 4471.iqtree.treefile
	 	
	You should see
	
		(RUTA_Citrus_hystrix@pg_uq:0.0967470193,(RUTA_Melicope_ternata@pg_uq:0.1621729005,(((((((((((MELI_Aglaia_spectabilis@pg_00:0.0379882798,MELI_Cabralea_canjerana@pg_00:0.0199533071):0.0085782116,(MELI_Chisocheton_longistipitatus@pg_00:0.0379882310,MELI_Aphanamixis_polystachya@pg_00:0.0494920662):0.0092253339):0.0021483280,MELI_Dysoxylum_alliaceum@pg_uq:0.0471504315):0.0015887986,MELI_Neoguarea_glomerulata@pg_01:0.0547080994):0.0008844444,MELI_Guarea_pubescens@pg_00:0.0533609950):0.0063054953,(((MELI_Aglaia_spectabilis@pg_02:0.0388463469,MELI_Cabralea_canjerana@pg_01:0.0216316868):0.0101132600,(MELI_Chisocheton_longistipitatus@pg_01:0.0387180305,((MELI_Heckeldora_staudtii@pg_00:0.0335110710,MELI_Neoguarea_glomerulata@pg_00:0.0618294687):0.0012785897,MELI_Guarea_pubescens@pg_02:0.0446490573):0.0018537144):0.0008490844):0.0027375406,MELI_Vavaea_amicorum@pg_00:0.0681955907):0.0029342096):0.0119221091,(MELI_Trichilia_hirta@pg_uq:0.0535061946,MELI_Turraea_virens@pg_uq:0.0851368654):0.0201718173):0.0016617099,((((MELI_Aglaia_spectabilis@pg_01:0.0519234782,MELI_Aphanamixis_polystachya@pg_01:0.0540052513):0.0009267065,MELI_Cabralea_canjerana@pg_02:0.0149007675):0.0150915790,(MELI_Guarea_pubescens@pg_01:0.0394354788,MELI_Heckeldora_staudtii@pg_01:0.0487069879):0.0065479564):0.0014578384,MELI_Vavaea_amicorum@pg_01:0.0835631202):0.0168885015):0.0115562485,MELI_Quivisianthe_papinae@pg_uq:0.0811917761):0.0341719786,((MELI_Azadirachta_indica@pg_uq:0.0004945456,MELI_Melia_azedarach@pg_uq:0.0015084365):0.0294961855,MELI_Owenia_reticulata@pg_uq:0.0294422745):0.0650087238):0.0047714922,((MELI_Swietenia_macrophylla@pg_uq:0.0692218925,(MELI_Toona_ciliata@pg_00:0.0225271377,MELI_Lovoa_sywnnertonii@pg_00:0.0531688410):0.0110747809):0.0144563047,((MELI_Toona_ciliata@pg_01:0.0268624674,MELI_Lovoa_sywnnertonii@pg_01:0.0711210879):0.0140801051,(MELI_Schmardaea_microphylla@pg_uq:0.0915458593,MELI_Chukrasia_tabularis@pg_uq:0.0562293914):0.0059356522):0.0049522269):0.0154278084):0.1260643977):0.0171517151,(RUTA_Ruta_graveolens@pg_00:0.0160212743,RUTA_Ruta_graveolens@pg_01:0.0230618982):0.1840426818);
	
	
<a name="masking"></a>
## Prune clades and paraphyletic grades of same species

* In this step were are going to mask clades and paraphyletic grades that belonged to the same taxon were pruned by keeping only the tip with the highest number of characters in the trimmed alignment

	First we are going to make a new directory called `03_masked`
	
		cd /data_tmp/mpemaster/data/07_phylogenomic_analyses
		
		mkdir 03_masked
		
* Now make sure that you are NOT in the Conda environment
	
	
		conda deactivate
		
	You should not see any conda environment name before you account name
	
		mpemaster@p620-small:/data_tmp/mpemaster/data/07_phylogenomic_analyses
		
	If you still see an Conda environment:
	
		(captus) mpemaster@p620-small:/data_tmp/mpemaster/data/07_phylogenomic_analyses
		
	or
	
		(base) mpemaster@p620-small:/data_tmp/mpemaster/data/07_phylogenomic_analyses
		
	run the below command until you don't see any envrioment
	
		conda deactivate
		
* Let's run the command to prune clade and paraphyletic grades of the same species

		python /data_tmp/mpemaster/script/mask_tips.py
		
	If you run this command you will see all the input arguments you need to provide. ####All Phython script we will use today will work the same way 
	
	The output should be
	
		python mask_tips.py treDIR tree_file_ending aln-clnDIR aln_cln_file_ending mask_paraphyletic(y/n) outDIR
		
	This script requires a input directory with the tree files, the file extension fo the tree files, whether or no you want to remove paraphyletic grades, and an output directory
	
	Make sure you are in the correct directory
	
		cd /data_tmp/mpemaster/data/07_phylogenomic_analyses
		
	Then
	
		python /data_tmp/mpemaster/script/mask_tips.py 02_raw_homolog_trees/ treefile 01_clean_alignments/ fna y 03_masked/
		
	This should be do done in seconds
	
	Now let's compare one original homologs vs a mask one
	
	
	



