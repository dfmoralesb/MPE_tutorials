## Table of contents

* [Concordance factors](#cf)
* [Quartet Sampling](#qs)
* [Conflict analysis with Phyparts](#phyparts)


#### How to login to the workstation

	ssh -p 22110 USERNAME@10.153.134.10


### Every time you see `$USERNAME` in the example command you need to replace it with you own [USERNAME](https://github.com/dfmoralesb/MPE_tutorials/blob/main/README.md)<br>

* To avoid having to change the `$USERNAME` for every command you can set a variable to provide the name of it. ***Do this every time you connect to the workstation***

	For example for me Diego my user name is `mpemaster`
	
		USERNAME=mpemaster


<a name="cf"></a>
## Alternative (complemental) node support values - Concordance factors

* When working with phylogenomic data sets, it is pretty common that tradicional node support values like bootstrap to be always high. This is due to the large amount of data available that make even known incorrect topologies to have high support, making this support measures inappropriate for large data sets. We want to understand the variation in the underlying data. There are several alternative and more appropriate node support measures that quantify for genealogical concordance like [Concordance factors in IQ-Tree](http://www.iqtree.org/doc/Concordance-Factor). For nice explanation on how to interpret concordance factors see [here](https://www.robertlanfear.com/blog/files/concordance_factors.html)

* IQ-Tree can calculate two kind of concordance factors. The gene concordance factor (gCF) and the site concordance factor (sCF). For every branch of a reference tree, gCF is defined as the percentage of “decisive” gene trees containing that branch. IQ-tree can calculate the gCF while accounting for missing data. sCF is defined as the percentage of "decisive" alignment sites supporting a branch in the reference tree. sCF is a novel measure that is particularly useful when individual gene alignments are relatively uninformative, such that gene trees are uncertain. gCF and sCF complement classical measures of branch support (e.g. bootstrap) in phylogenetics by providing a full description of underlying disagreement among loci and sites. 

* To calculate concordance factors you need a reference trees (e.g. concatenated tree or coalescent-based tree; it could be any tree for that matter) and the individual ortholog gene trees (gCF) and the concatenated ortholog alignment (sCF)

	Load the conda environment 
	
		conda actiavate captus
	
	Make a new directory where we will run IQ-tree
	
		cd /data_tmp/mpemaster/data/07_phylogenomic_analyses
	
		mkdir 11_concordance_factors
		
		cd 11_concordance_factors
		
	Now we can run IQ-tree to get the gCF and sCF using the concatenated tree as reference tree. Remember from the previous tutorial that the tree should be located in `/data_tmp/$USERNAME/output/04_analyses/10_iqtree_concatenated` The gene trees will be the same input trees file we use for ASTRAL in the previous tutorial located in `/data_tmp/mpemaster/data/07_phylogenomic_analyses/07_astral` use the non-collapse one `meliaceae_334_MO_orthologs.tre` And the concatenated alignment is located in `/data_tmp/mpemaster/data/07_phylogenomic_analyses/08_concatenated_aln`
	
		iqtree -te /data_tmp/$USERNAME/output/04_analyses/10_iqtree_concatenated/meliaceae_MO_500_8_concat_IQtree.treefile --gcf /data_tmp/mpemaster/data/07_phylogenomic_analyses/07_astral/meliaceae_334_MO_orthologs.tre --scf 1000 -T 4 -s /data_tmp/mpemaster/data/07_phylogenomic_analyses/08_concatenated_aln/meliaceae_MO_500_8_concat.fa --prefix meliaceae_MO_500_8_concat_IQtree

		/home/morales/Apps/iqtree-2.0.7-Linux/bin/iqtree2 -t DATA/IQ-tree_concatenated/output/IQtree2_concatenated_2419_loci.iqtree -s DATA/IQ-tree_concatenated/input/concatenated_2419_loci.phy --scf 100 --prefix DATA/IQ-tree_concatenated/output/sCF_concord -T 8
		
	You should start seeing
	
	
		IQ-TREE multicore version 2.4.0 for Linux x86 64-bit built Feb 12 2025
		Developed by Bui Quang Minh, Nguyen Lam Tung, Olga Chernomor, Heiko Schmidt,
		Dominik Schrempf, Michael Woodhams, Ly Trong Nhan, Thomas Wong
		
		Host:    p620-small (AVX2, FMA3, 251 GB RAM)
		Command: iqtree -te /data_tmp/mpemaster/output/04_analyses/10_iqtree_concatenated/meliaceae_MO_500_8_concat_IQtree.treefile --gcf /data_tmp/mpemaster/data/07_phylogenomic_analyses/07_astral/meliaceae_334_MO_orthologs.tre --scf 1000 -T 4 -s /data_tmp/mpemaster/data/07_phylogenomic_analyses/08_concatenated_aln/meliaceae_MO_500_8_concat.fa --prefix meliaceae_MO_500_8_concat_IQtree
		Seed:    147240 (Using SPRNG - Scalable Parallel Random Number Generator)
		Time:    Tue Feb 25 16:03:17 2025
		Kernel:  AVX+FMA - 4 threads (64 CPU cores detected)
		...
	
	It should take 2 to 3 minutes to complete the run
	
	The file you can to plot in Fig tree is `meliaceae_MO_500_8_concat_IQtree.cf.tree`
	
		cat meliaceae_MO_500_8_concat_IQtree.cf.tree 
		
		(RUTA_Citrus_hystrix:0.1203095997,(RUTA_Melicope_ternata:0.1713673116,(((((((((((MELI_Aglaia_spectabilis:0.0375885764,MELI_Aphanamixis_polystachya:0.0419670632)100/64/43.2:0.0056021936,MELI_Cabralea_canjerana:0.0255826820)100/57.1/50.1:0.0046142662,MELI_Dysoxylum_alliaceum:0.0482585193)100/40.8/40.7:0.0026290050,MELI_Chisocheton_longistipitatus:0.0434381144)100/26/37.5:0.0016593652,((MELI_Heckeldora_staudtii:0.0427502585,MELI_Guarea_pubescens:0.0411445158)88/14.9/37.4:0.0007827064,(MELI_Neoguarea_glomerulata:0.0451238849,MELI_Turraeanthus_manii:0.0560241287)97/14.7/29.7:0.0018363755)100/31.8/37.3:0.0023701151)100/48.6/46.7:0.0060012439,MELI_Vavaea_amicorum:0.0762391468)100/55.6/43.6:0.0077188462,(MELI_Trichilia_hirta:0.0527954546,MELI_Turraea_virens:0.1002290411)100/89/52.7:0.0208684956)100/47.6/42.4:0.0092840998,MELI_Munronia_pinnata:0.0763143712)100/70.1/44.6:0.0115924912,MELI_Quivisianthe_papinae:0.0927838334)100/93/59.1:0.0330980586,(((MELI_Azadirachta_indica:0.0028085964,MELI_Melia_azedarach:0.0042547263)100/100/96.8:0.0325065738,MELI_Owenia_reticulata:0.0372445257)100/92.7/64.4:0.0189203949,MELI_Pterorhachis_zenkeri:0.0506308134)100/98.4/73.8:0.0601215172)100/45.3/34.9:0.0068608865,((((MELI_Toona_ciliata:0.0209736796,(MELI_Cedrela_montana:0.0246820354,MELI_Cedrela_saltensis:0.0106038088)100/100/76.9:0.0356809672)100/81.8/71.3:0.0186519042,MELI_Lovoa_sywnnertonii:0.0681119901)100/61.3/39.2:0.0045679476,((MELI_Swietenia_macrophylla:0.0124428947,MELI_Swietenia_mahagoni:0.0307433133)100/93.3/92.1:0.0231644117,MELI_Carapa_procera:0.0308532123)100/98.2/78.5:0.0385898559)100/88.6/53.3:0.0154981841,(MELI_Schmardaea_microphylla:0.0977996692,MELI_Chukrasia_tabularis:0.0568456093)100/74.5/41.9:0.0103559063)100/89.7/55.5:0.0261171806)100/100/70.1:0.0969635918)100/54.9/36.8:0.0173378156,RUTA_Ruta_graveolens:0.2229865468);

	<p align="center"><img src="images/cf.png" alt="cf" width="900"></p>

	You can see that the node have three values. The first one is the ultrafast bootstrap fron the original tree inference, the second the gCF, and the third the sCF.
		
		
* gCF range grom 0% no gene trees support that node to 100% all gene tress support that node.

* In principle, sCF values can range from 0% (no sites are concordant with the focal branch) to 100% (all sites are concordant with the focal branch). In practice however, empirical sCF values are rarely lower than 33%. This is due to an important underlying difference in the way that the two values are calculated. The sCF is calculated from quartets, so a single site can only support one of three topologies. Because of this, if there is no consistent information in an alignment (e.g., if a long alignment were generated at random) we expect a roughly equal proportion of sites supporting each of the three trees, leading to an sCF value of ∼33%. 




	The output files for the IQ-tree run can be found here `/data_tmp/$USERNAME/output/04_analyses/10_iqtree_concatenated`
	
	Plot the tree file and compare it with the ASTRAL species trees from above
	
		cat /data_tmp/$USERNAME/output/04_analyses/10_iqtree_concatenated/meliaceae_MO_500_8_concat_IQtree.treefile
		
		(RUTA_Citrus_hystrix:0.1203095997,(RUTA_Melicope_ternata:0.1713673116,(((((((((((MELI_Aglaia_spectabilis:0.0375885764,MELI_Aphanamixis_polystachya:0.0419670632)100:0.0056021936,MELI_Cabralea_canjerana:0.0255826820)100:0.0046142662,MELI_Dysoxylum_alliaceum:0.0482585193)100:0.0026290050,MELI_Chisocheton_longistipitatus:0.0434381144)100:0.0016593652,((MELI_Heckeldora_staudtii:0.0427502585,MELI_Guarea_pubescens:0.0411445158)88:0.0007827064,(MELI_Neoguarea_glomerulata:0.0451238849,MELI_Turraeanthus_manii:0.0560241287)97:0.0018363755)100:0.0023701151)100:0.0060012439,MELI_Vavaea_amicorum:0.0762391468)100:0.0077188462,(MELI_Trichilia_hirta:0.0527954546,MELI_Turraea_virens:0.1002290411)100:0.0208684956)100:0.0092840998,MELI_Munronia_pinnata:0.0763143712)100:0.0115924912,MELI_Quivisianthe_papinae:0.0927838334)100:0.0330980586,(((MELI_Azadirachta_indica:0.0028085964,MELI_Melia_azedarach:0.0042547263)100:0.0325065738,MELI_Owenia_reticulata:0.0372445257)100:0.0189203949,MELI_Pterorhachis_zenkeri:0.0506308134)100:0.0601215172)100:0.0068608865,((((MELI_Toona_ciliata:0.0209736796,(MELI_Cedrela_montana:0.0246820354,MELI_Cedrela_saltensis:0.0106038088)100:0.0356809672)100:0.0186519042,MELI_Lovoa_sywnnertonii:0.0681119901)100:0.0045679476,((MELI_Swietenia_macrophylla:0.0124428947,MELI_Swietenia_mahagoni:0.0307433133)100:0.0231644117,MELI_Carapa_procera:0.0308532123)100:0.0385898559)100:0.0154981841,(MELI_Schmardaea_microphylla:0.0977996692,MELI_Chukrasia_tabularis:0.0568456093)100:0.0103559063)100:0.0261171806)100:0.0969635918)100:0.0173378156,RUTA_Ruta_graveolens:0.2229865468);
