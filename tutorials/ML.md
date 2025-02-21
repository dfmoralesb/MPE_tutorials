## Table of contents

* [Maximum-likelihood phylogenetic inference with IQ-TREE](#iqtree)
* [Reading and visualizing tree files](#figtree)
* [Assessing node support with bootstrapping](#boot)
* [Inferring a concatenated ML tree](#concat)
* [Alternative node support values - Concordance factors](#concordance)

### Every time you see `[username]` in the example command you need to replace it with you own [username](https://github.com/dfmoralesb/MPE_tutorials/blob/main/README.md)<br>

Make sure to activate the `CONDA` environment

	conda activate captus

<a name="iqtree"></a>
## Maximum-likelihood phylogenetic inference with IQ-TREE

Maximum-likelihood phylogenetic inference aims to find the parameters of an evolutionary model that maximize the likelihood of observing the dataset at hand. The model parameters include the tree topology and its branch lengths but also all parameter of the substitution model (e.g., GTR) assumed in the inference. 

* To see the many options available in IQ-TREE you can type the following in the command line:

		iqtree --help

* You can scroll up and down to check all the available options. <p align="center"><img src="images/Iqtree_1.png" alt="IQTREE" width="900"></p>		
		
* IQ-TREE can be started just by providing the alignment name. We can try this with one of the individual alignments. IQ-TREE will run a default analyses (i.e. Model selection followed of ML inference using one CPU)

		cd /data_tmp/[username]/data/04_individual_aln

		iqtree -s 4471.aln.clipkit 
		
	As you'll see, just providing the alignment name is sufficient to run a simple IQ-TREE analyses. The analysis should be done in a minute.
	
	<p align="center"><img src="images/Iqtree_2.png" alt="IQTREE" width="900"></p>		

* Scroll to the end of the IQ-TREE output. There, you'll find parameter estimates for the selected substitution model, the maximum-likelihood value (given as logarithm after "BEST SCORE FOUND"), information on the run time, and the names of output files.

* According to the IQ-TREE screen output, the best-scoring maximum-likelihood tree was written to file `4471.aln.clipkit.treefile`

	<p align="center"><img src="images/Iqtree_3.png" alt="IQTREE" width="900"></p>

* All output file names were automatically chosen based on the name of the input file. This be changed this using the `--prefix` option.

<a name="figtree"></a>
## Reading and visualizing tree files

Here we will explore how phylogenetic trees are encoded in Newick format, the most commonly used format in phylogenetic sofware, and we will visualize the maximum-likelihood phylogeny generated with IQ-TREE with the program [FigTree](http://tree.bio.ed.ac.uk/software/figtree/). For more detail about the newick format see [here](https://phylipweb.github.io/phylip/newicktree.html).

* Open the file `4471.aln.clipkit.treefile` in a text editor, or on the command line using, for example, the `cat` command:

		less 4471.aln.clipkit.treefile
		
	You'll see a long string containing the taxon IDs, each of which is followed by a colon and a number, and together with these, the taxon IDs are embedded in parentheses.
		
		(MELI_Aglaia_spectabilis__00:0.0380179390,(((((((((((MELI_Aglaia_spectabilis__01:0.0506739175,MELI_Aphanamixis_polystachya__01:0.0535434293):0.0009582787,MELI_Cabralea_canjerana__02:0.0140979167):0.0148666359,(MELI_Guarea_pubescens__01:0.0393937815,MELI_Heckeldora_staudtii__01:0.0480125875):0.0064761451):0.0012831257,MELI_Vavaea_amicorum__01:0.0825715324):0.0169487786,(((((MELI_Azadirachta_indica:0.0004927154,MELI_Melia_azedarach:0.0020470950):0.0287155251,MELI_Owenia_reticulata:0.0313943437):0.0190395806,MELI_Pterorhachis_zenkeri:0.0425344882):0.0463844845,((((MELI_Carapa_procera:0.0243152104,MELI_Swietenia_macrophylla:0.0331743798):0.0364456250,(MELI_Lovoa_sywnnertonii__00:0.0534910638,MELI_Toona_ciliata__00:0.0222303545):0.0112998021):0.0146482776,((MELI_Chukrasia_tabularis:0.0603985313,MELI_Schmardaea_microphylla:0.0932356732):0.0059751090,(MELI_Lovoa_sywnnertonii__01:0.0715604163,MELI_Toona_ciliata__01:0.0270178220):0.0144402397):0.0049209856):0.0162916902,((RUTA_Citrus_hystrix:0.0955127303,(RUTA_Ruta_graveolens__00:0.0155031330,RUTA_Ruta_graveolens__01:0.0242888190):0.1909844938):0.0167509809,RUTA_Melicope_ternata:0.1640001395):0.1252373604):0.0051787758):0.0337809330,MELI_Quivisianthe_papinae:0.0833022953):0.0114346424):0.0016806024,(MELI_Trichilia_hirta:0.0527888671,MELI_Turraea_virens:0.0849778741):0.0198736252):0.0117351016,(((MELI_Aglaia_spectabilis__02:0.0392266628,MELI_Cabralea_canjerana__01:0.0213777247):0.0096306741,(MELI_Chisocheton_longistipitatus__01:0.0385910779,(MELI_Guarea_pubescens__02:0.0440549647,(MELI_Heckeldora_staudtii__00:0.0340058439,(MELI_Neoguarea_glomerulata__00:0.0617785610,MELI_Turraeanthus_manii:0.0430127959):0.0016654293):0.0005171647):0.0020616325):0.0010408630):0.0030760053,MELI_Vavaea_amicorum__00:0.0684560127):0.0027216237):0.0060321840,MELI_Guarea_pubescens__00:0.0535230595):0.0008256918,MELI_Neoguarea_glomerulata__01:0.0498438147):0.0017009200,MELI_Dysoxylum_alliaceum:0.0457100313):0.0021620938,(MELI_Aphanamixis_polystachya__00:0.0498633453,MELI_Chisocheton_longistipitatus__00:0.0379487095):0.0092600438):0.0086872234,MELI_Cabralea_canjerana__00:0.0201619645);
		
* Open FigTree, copy the above tree string and paste it into a new FigTree window. You'll see a phylogeny as shown in the screenshot below.

<p align="center"><img src="images/figtree_1.png" alt="FigTree" width="900"></p>

* To correct the rooting of the phylogeny, we can specify an outgroup. In case we are going to use the samples of Rutaceae. Click on the branch leading to "RUTA_Citrus_hystrix, RUTA_Ruta_graveolens, and RUTA_Melicope_ternata", as shown in the next screenshot.

<p align="center"><img src="images/figtree_2.png" alt="FigTree" width="900"></p>

* Then, with that branch being selected, click on the "Reroot" icon with the yellow arrow in the menu bar. The phylogeny should then look as shown in the next screenshot.

<p align="center"><img src="images/figtree_3.png" alt="FigTree" width="900"></p>

* Finally, we could sort the taxa according to node order. To do so, select "Order nodes" -> "increasing" in FigTree's "Tree" menu. This should move Rutaceae to the bottom of the plot

<p align="center"><img src="images/figtree_4.png" alt="FigTree" width="900"></p>

* If instead you use "Order nodes" -> "decreasing" then Rutaceae would be on the top of the plot. Both phylogenies are exactly the same, the relationship do not change. How you order the nodes is a matter of preference.

<p align="center"><img src="images/figtree_5.png" alt="FigTree" width="900"></p>

<a name="boot"></a>
## Assessing node support with bootstrapping

To identify which nodes in the phylogeny are more or less trustworthy, we will now perform a bootstrap analysis.

* To see again the available options in IQ-TREE type:

		iqtree --help

* Scroll towards the top of the help text, there you should find two sections titled "ULTRAFAST BOOTSTRAP/JACKKNIFE" and "NON-PARAMETRIC BOOTSTRAP/JACKKNIFE". In this occasion we are going to use the `-B` option to perform [Ultrafast Bootstrap](https://academic.oup.com/mbe/article/35/2/518/4565479) which is a significantly fast implementation of the standard non-parametric bootstrap [Felsenstein, 1986](https://doi.org/10.1111/j.1558-5646.1985.tb00420.x). 


		 iqtree  -s 4471.aln.clipkit -B 100 --prefix 4471.aln.clipkit.bootstrap -T 4
	
		
* This command will run the 100 replicates for the ultrafast bootstrap + ML tree + consensus tree. Note that we are using the `--prefix` option to rename the output files. Otherwise the file names would be the same as in the previous run and IQ-TREE will produced an error and will ask to rewrite those files. The prefix not only provides the name of the files but also the directory path for the location of the output files.

	The analysis should be done in in a minute or so.

* Open file `4471.aln.clipkit.bootstrap.treefile` in FigTree. You can use the `cat` command as before and copy and paste the tree string on FigTree.

		cat 4471.aln.clipkit.bootstrap.treefile
		
	It should look like this:		
		
		(MELI_Aglaia_spectabilis__00:0.0380191497,(((((((((((MELI_Aglaia_spectabilis__01:0.0506752054,MELI_Aphanamixis_polystachya__01:0.0535450023)89:0.0009585045,MELI_Cabralea_canjerana__02:0.0140978502)100:0.0148672057,(MELI_Guarea_pubescens__01:0.0393964385,MELI_Heckeldora_staudtii__01:0.0480148296)97:0.0064759238)79:0.0012827492,MELI_Vavaea_amicorum__01:0.0825759821)100:0.0169494621,(((((MELI_Azadirachta_indica:0.0004927390,MELI_Melia_azedarach:0.0020471203)100:0.0287150227,MELI_Owenia_reticulata:0.0313953162)100:0.0190407336,MELI_Pterorhachis_zenkeri:0.0425364445)100:0.0463861504,((((MELI_Carapa_procera:0.0243155357,MELI_Swietenia_macrophylla:0.0331749157)100:0.0364473094,(MELI_Lovoa_sywnnertonii__00:0.0534921501,MELI_Toona_ciliata__00:0.0222309475)100:0.0112997555)100:0.0146492009,((MELI_Chukrasia_tabularis:0.0604013008,MELI_Schmardaea_microphylla:0.0932412654)89:0.0059747898,(MELI_Lovoa_sywnnertonii__01:0.0715635995,MELI_Toona_ciliata__01:0.0270192067)99:0.0144402359)98:0.0049197057)100:0.0162920912,((RUTA_Citrus_hystrix:0.0955186534,(RUTA_Ruta_graveolens__00:0.0155041122,RUTA_Ruta_graveolens__01:0.0242876157)100:0.1910002272)93:0.0167476141,RUTA_Melicope_ternata:0.1640168719)100:0.1252496621)94:0.0051790366)100:0.0337816812,MELI_Quivisianthe_papinae:0.0833058020)100:0.0114346130)70:0.0016805028,(MELI_Trichilia_hirta:0.0527898689,MELI_Turraea_virens:0.0849819570)100:0.0198736602)100:0.0117354579,(((MELI_Aglaia_spectabilis__02:0.0392278898,MELI_Cabralea_canjerana__01:0.0213782169)100:0.0096307368,(MELI_Chisocheton_longistipitatus__01:0.0385930601,(MELI_Guarea_pubescens__02:0.0440566759,(MELI_Heckeldora_staudtii__00:0.0340066527,(MELI_Neoguarea_glomerulata__00:0.0617810110,MELI_Turraeanthus_manii:0.0430148729)47:0.0016660968)53:0.0005168096)56:0.0020618474)69:0.0010400015)93:0.0030760948,MELI_Vavaea_amicorum__00:0.0684575517)96:0.0027216476)100:0.0060321857,MELI_Guarea_pubescens__00:0.0535240875)80:0.0008254210,MELI_Neoguarea_glomerulata__01:0.0498460103)85:0.0017009147,MELI_Dysoxylum_alliaceum:0.0457119769)89:0.0021621374,(MELI_Aphanamixis_polystachya__00:0.0498655165,MELI_Chisocheton_longistipitatus__00:0.0379500863)48:0.0092601942)55:0.0086864611,MELI_Cabralea_canjerana__00:0.0201624965);

* Open the file or copy and paste in FigTree. Root the tree with Rutaceae and sort the nodes as before. 

* To see node-support values based on bootstrapping, set a tick in the checkbox for "Node Labels", and select "label" from the "Display" drop-down menu, as shown in the below screenshot. 

<p align="center"><img src="images/figtree_6.png" alt="FigTree" width="900"></p>



















* To estimate a coalescent-based species tree with ASTRAL, we need to infer the indvidual ML gene trees for each of the 2420 alignments in the folder `DATA/IQ-tree_individual_loc/input`. 

	You do not need to do this as all the output files are already located in `DATA/IQ-tree_individual_loc/output`. But you could do it with a bash loop like:
	
	
		for i in $(ls *.phy)
		do
		iqtree2 -s $i -b 200
		done

<a name="concat"></a>
## Inferring a concatenated ML tree

Here we are going to infer a ML tree with IQ-tree using a concatenated alignment of the 2419 loci. The input data is located in `DATA/IQ-tree_concatenated/input`.

* You can see the size of the concatenated matrix by typing.

		head -n 1 DATA/IQ-tree_concatenated/input/concatenated_2419_loci.phy
		
* You will see printed on the screen the below line. That means that the alignment contains 21 taxa and 848730 aligned columns.

		21 848730
		
* In this case we are going to use do a Partitioned maximum-likelihood inference. This means that we are going to split the alignment by loci and allow IQ-TREE to determine the ideal partitioning scheme itself. For this new need a 'partion' file and the option `q`. The partion file is located in the same directory as the alignment. 

You can see the beginning (head) of the file by typing.

		 head DATA/IQ-tree_concatenated/input/concatenated_aln.model
		 
And also can see the end (tail) 

		tail DATA/IQ-tree_concatenated/input/concatenated_aln.model

<p align="center"><img src="images/partition.png" alt="partition" width="900"></p>

	
The partition file specifies the kind of partition `DNA` a unique name of each partion (e.g. `fasta_files/Locus_597.x.phy.fa;` this is just the name of the original alignment file) and the size of each partition (i.e. the range of the each partion in the alignment).

* To tell IQ-TREE to determine the ideal partitioning scheme itself, we need to use the options `-m MFP --merge`. This tells IQ-TREE to perform model selection on each partition and combine similar partiton to find the best scheme. This uses the implementation of Kalyaanamoorthy et al. ([2017](http://dx.doi.org/10.1038/nmeth.4285))

* In this occasion we are going to use ultrafast bootstrap procedure with the `-B` option. IQ-TREE recommends a a minimum of 1,000 replicates, but IQ-TREE will automatically reduce this number if it detects that the resulting node-support values are stable also after a lower number of replicates. See Hoang et al. ([2017](https://academic.oup.com/mbe/article/35/2/518/4565479)) for more details. 


		/home/morales/Apps/iqtree-2.0.7-Linux/bin/iqtree2  -m MFP --merge -s concatenated_2419_loci.fa -T 120 -B 1000 -q concatenated_aln.model --prefix DATA/IQ-tree_concatenated/output/IQtree2_concatenated_2419_loci

* Running this analysis should be considerabl longer than the previous analysis of one individual locus. One way to speed things up is running IQ-TREE using multiple CPUs with the `-T` options. In this case, I will use `-T 120`. If not sure about the number of CPUs available you can use `-T AUTO`

* You do not need to run this as it will take too much time. The output files for this analyses are located at `DATA/IQ-tree_concatenated/output`.

* Open the file `IQtree2_concatenated_2419_loci.treefile`

		less DATA/IQ-tree_concatenated/output/IQtree2_concatenated_2419_loci.treefile

	It should look like this:		
		
		(A_arboreum_153:0.0014849078,(A_balsamiferum_TM178:0.0011535530,(((((A_cuneatum_134:0.0065514518,A_canariense_TM189:0.0072583511)100:0.0015530642,Aeo_glutinosum:0.0090574484)100:0.0023872758,(((((A_ciliatum_135:0.0026558778,A_volkerii_TM194:0.0024888707)100:0.0009839747,A_urbicum_TM2001:0.0042130349)100:0.0012161129,Aeo_haworthii:0.0022985151)100:0.0014098253,A_davidbramwellii_TM2021:0.0056304679)100:0.0023965907,(A_valverdense_TM2131:0.0052622481,A_nobile_TM191:0.0082347492)100:0.0020565574)100:0.0032489645)87:0.0016314676,(((A_goochiae_TM184:0.0064710978,A_lindleyi_TM190:0.0061792425)100:0.0097779590,Mon_mura_111:0.0434930391)84:0.0012266869,(A_saundersii_merged:0.0128397974,A_sedifolium_TM187:0.0140337688)100:0.0025872713)100:0.0048456363)100:0.0053188993,((A_stuessyi_TM2031:0.0005572773,A_leucoblepharu:0.0009037328)99:0.0006215380,A_gorgoneum_TM185:0.0010816831)100:0.0022975052)100:0.0054524452)100:0.0008226453,Aeo_korneliuslemsii:0.0019086054);
	
* Open the file in FigTree, root tit with "Mon_mura_111", sort the taxa with "Increasing node order" and display the node support. You can see how the brach lengths and bootstrap support differ from a single-locus tree. <p align="center"><img src="images/concat.png" alt="partition" width="900"></p>



<a name="concordance"></a>
## Alternative node support values - Concordance factors

* When working with phylogenomic data sets, it is pretty common that tradicional node support values like bootstrap to be always high. This is due to the large amount of data available that make even known incorrect topologies to have high support, making this support measures inappropriate for large data sets. Now there are several alternative and more appropriate node support measures that quantify for genealogical concordance like [Concordance factors in IQ-Tree](http://www.iqtree.org/doc/Concordance-Factor).

* To calculate concordance factors in IQ-Tree you need the concatenated alignment and the inferred tree. You can run IQ-Tree like:

		/home/morales/Apps/iqtree-2.0.7-Linux/bin/iqtree2 -t DATA/IQ-tree_concatenated/output/IQtree2_concatenated_2419_loci.iqtree -s DATA/IQ-tree_concatenated/input/concatenated_2419_loci.phy --scf 100 --prefix DATA/IQ-tree_concatenated/output/sCF_concord -T 8
		
To open the file

	less DATA/IQ-tree_concatenated/output/sCF_concord.cf.tree
		
* Open the file `sCF_concord.cf.tree` in Figtree, rooted and display the "Node labels"
<p align="center"><img src="images/concon.png" alt="partition" width="900"></p>

* In principle, sCF values can range from 0% (no sites are concordant with the focal branch) to 100% (all sites are concordant with the focal branch). In practice however, empirical sCF values are rarely lower than 33%. This is due to an important underlying difference in the way that the two values are calculated. The sCF is calculated from quartets, so a single site can only support one of three topologies. Because of this, if there is no consistent information in an alignment (e.g., if a long alignment were generated at random) we expect a roughly equal proportion of sites supporting each of the three trees, leading to an sCF value of ∼33%. 


