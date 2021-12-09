# Phylogenetic Divergence-Time Estimation

## Table of contents

* [Divergence time estimation with BEAST2](#beast)
* [Setting the XML file with BEAUti](#beaut)
* [Running BEAST](#beast)
* [Assessing MCMC stationarity with Tracer](#tracer)
* [Summarizing the posterior tree distribution](#treeannotator)

<a name="beast"></a>
## Divergence time estimation with BEAST2

* Here we will infer ttime-calibrated phylogenies can be inferred with programs of the Bayesian software package [BEAST2](https://www.beast2.org) ([Bouckaert et al. 2014](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1003537)). The settings for the analysis will be done with the program BEAUti, the Bayesian analysis itself is going to be conducted with BEAST2, and a summary tree will be generated with the program TreeAnnotator. These three programs are part of the BEAST2 package. Finally, we explote the use of the program [Tracer](http://beast.community/tracer) ([Rambaut et al. 2018](https://academic.oup.com/sysbio/advance-article/doi/10.1093/sysbio/syy032/4989127)) to assess stationarity and convergence of the Bayesian analysis.


* If you are not familiar  with Bayesian analyses and Markov-Chain Monte Carlo methods in general, you can explore the many resources made available by BEAST2 authors. You can also explore the [BEAST2 website](https://www.beast2.org) and quickly browse through the [glossary of terms related to BEAST2 analyses](https://www.beast2.org/glossary/index.html). The BEAST2 website also provides a [wide range of tutorials and manuals](https://www.beast2.org/tutorials/index.html). Also, you can find comprehensive tutorials on the [Taming the BEAST](https://taming-the-beast.org) website, where you will also find information about the excellent [Taming-the-BEAST workshops](https://taming-the-beast.org/workshops/). 

* We will be using the same data set we used for the concatenated phylogeny with IQ-TREE. All input and out files will be located in the directory `DATA/BEAST`

<a name="beaut"></a>
## Setting the XML file with BEAUti

* The XML [Extensible Markup Language](https://www.w3.org/standards/xml/core) files contains the alignement, priors, and other setting to run the analyses on BEAST.

* Open the program BEAUti and import the alignment `FcC_supermatrix.nex`. To do so, click "Import Alignment" from the "File" menu and select the the file `DATA/BEAST/input/FcC_supermatrix.nex` The BEAUti window should then look as shown in the screenshot below. There you can see the number of taxa, alignment length, and any data partition. In this case we are not using any partion. <p align="center"><img src="images/beauti_1.png" alt="beauti" width="900"></p>

* Next, click on the "Site Model" tab next. In this tab we can specify the substitution model. Now, click on the drop-down menu that currently says "JC69". Instead of the Jukes-Cantor model, use the GTR model. Also specify "4" in the field for the "Gamma Category Count" two lines above, to use a gamma model of rate variation with four rate categories. Finally, set a tick in the checkbox to the right of "Substitution Rate" so that this rate will be estimated.The BEAUti window should then look as shown in the screenshot below.<p align="center"><img src="images/beauti_2.png" alt="beauti" width="900"></p>

* Next, click on the "Clock Model" tab. From the drop-down menu that currently says "Strict Clock", choose "Relaxed Clock Log Normal" instead. This is the most commonly used relaxed clock model in which substitution rates of individual branches are drawn from a lognormal distribution. Also set a tick in the checkbox on the right side of the window. If this checkbox appears gray and you are unable to set it, you'll need to click on "Automatic set clock rate" in BEAUti's "Mode" menu. The mean and standard deviation of this lognormal distribution will be estimated as part of the MCMC search. The model is described in [Drummond et al. (2006)](http://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.0040088), there it is named the "UCLN" model. Ignore the additional options ("Number of Discrete Rates" etc.) that appear after selecting the model.<p align="center"><img src="images/beauti_3.png" alt="beauti" width="900"></p>

* Click on the "Priors" tab. From the drop-down menu at the very top of the window, select "Birth Death Model" instead of "Yule Model". By doing so we add a parameter to the model for the extinction rate. If we would choose the alternative Yule model ([Yule 1925](http://rstb.royalsocietypublishing.org/content/213/402-410/21?intcmp=trendmd)), we would assume that no extinction ever occurred. As this seems rather unrealistic, the birth-death model ([Gernhard 2008](https://www.sciencedirect.com/science/article/pii/S0022519308001811)) is in most cases the more appropriate choice. Nevertheless, results are in practice rather little affected by the choice of this prior.

* Most of the other items shown in the "Prior" panel correspond to prior densities placed on the parameters of the substitution models for the four partitions. You may keep the default priors for each of these parameters. However, to allow time calibration of the phylogeny, a prior density still needs to be specified for at least one divergence time, otherwise BEAST2 would have very little information (only from the priors on speciation and mutation rates) to estimate branch lengths according to an absolute time scale. But before prior densities can be placed on the divergence of certain clades, these clades must first be defined. This can be done at the bottom of the "Priors" tab. Thus, scroll down to the end of the list until you see the "+ Add Prior" button, as shown in the below screenshot.<p align="center"><img src="images/beauti_4.png" alt="beauti" width="900"></p>

* Click on the "+ Add Prior" button to open the "Taxon set editor" pop-up window. Select all taxa from the list on the left of that window, and click the double-right-arrow symbol (`>>`) to shift them to the right side of the window. This way, the ingroup, including all taxa, so that the divergence between the root and *Aeonium* can later be used for time calibration. Enter "Crown" for name at the top of the pop-up window as the "Taxon set label", as shown in the below screenshot. Then, click "OK".<p align="center"><img src="images/beauti_5.png" alt="beauti" width="900"></p>

* To time calibrate this divergence, click on the drop-down menu to the right of the button for "Crown.prior" that currently says "[none]". Then, click on the black triangle to the left of the button for "Crown.prior". Specify "11.62" as the value for "M" (that is the mean of the prior density) and "0.25" as the value for "S" (that is the standard deviation). Importantly, set a tick in the checkbox for "Mean in Real Space"; otherwise, the specified value for the mean will be considered to be in log space (meaning that its exponent would be used). In the plot to the right, you should then see that the density is centered around 11. The BEAUti window should then look as shown in the below screenshot.<p align="center"><img src="images/beauti_6.png" alt="beauti" width="900"></p>


* Continue to the "MCMC" tab, where you can specify the run length. This analysis will require a few hundred million iterations before the MCMC chain reaches full stationarity, which would take several days of run time. We run this in advance and output fill will be located at `DATA/BEAST/input/`. Type "200000000" in the field to the right of "Chain Length".

	Also change the names of the output files: Click on the triangle to the left of "tracelog" and specify "FcC_supermatrix.log" as the name of the log file, probably it will be filed automatically.In the next field for "Log Every", set the number to "5000" (instead of the default 1,000) so that only every 5,000th MCMC state is written to the log file. Click on the black triangle to the left of "screenlog" and use "5000" for Log Every". Then click on the black triangle to the left of "treelog". Specify leave 'File Name' as it is and again use "5000" as the number in the field for "Log Every". 
	
	<p align="center"><img src="images/beauti_7.png" alt="beauti" width="900"></p>
	<p align="center"><img src="images/beauti_8.png" alt="beauti" width="900"></p>

		
* When the window looks as in the above screenshots, click on "Save" in BEAUti's "File" menu, and name the resulting file in XML format `Aeonium_BEAST2.xml`.	<p align="center"><img src="images/beauti_9.png" alt="beauti" width="900"></p>

<a name="beast"></a>
## Running BEAST

* Open the program BEAST2 and select the file [`Aeonium_BEAST2.xml` as input file, as shown in the screenshot below. When you click the "Run" button, BEAST2 will start the analysis. Running BEAST2 in this way is not convient as it usually takes several day, but it is helpful to see if the XML was correctly set up and BEAST starts without problem.

<p align="center"><img src="images/beast_1.png" alt="beast" width="500"></p>

* Usually BEAST2 is run in a workstation or cluster using the command line like

		~/Apps/beast/bin/beast -threads 30 DATA/BEAST/input/Aeonium_BEAST2.xml
		
	If BEAST2 started to run correctly you will see something like this:<p align="center"><img src="images/beast_2.png" alt="beast" width="900"></p>
	
	
<a name="tracer"></a>
## Assessing MCMC stationarity with Tracer

*	In Bayesian analyses with the software BEAST2, it is rarely possible to tell *a priori* how many MCMC iterations will be required before the analysis can be considered complete. Instead, whether or not an analysis is complete is usually decided based on the inspection of the log file once BEAST2 has performed the specified number of MCMC iterations. There are various ways in which MCMC output can be used to assess whether or not an analysis can be considered complete, and in the context of phylogenetic analyses with BEAST2, the most commonly used diagnostic tools are those implemented in [Tracer](http://beast.community/tracer) ([Rambaut et al. 2018](https://academic.oup.com/sysbio/advance-article/doi/10.1093/sysbio/syy032/4989127)) or the R package [coda](https://cran.r-project.org/web/packages/coda/index.html) ([Plummer et al. 2006](https://cran.r-project.org/doc/Rnews/Rnews_2006-1.pdf#page=7)). Here, we are going to investigate run completeness with Tracer. Ideally, we should have conducted the same BEAST2 analysis multiple times; then, we could assess whether the replicate MCMC chains "converge" to the same posterior distribution, which would be a requirement for a complete MCMC analysis. I performed in advance two independent BEAST runs found in the directory `DATA/BEAST/input/`

In Tracer you can do the following:

1. Calculation of "effective sample sizes" (ESS). Because consecutive MCMC iterations are always highly correlated, the number of effectively independent samples obtained for each parameter is generally much lower than the total number of sampled states. Calculating ESS values for each parameter is a way to assess the number of independent samples that would be equivalent to the much larger number of auto-correlated samples drawn for these parameters. These ESS values are automatically calculated for each parameter by Tracer. As a rule of thumb, the ESS values of all model parameters, or at least of all parameters of interest, should be above 200.
2. Visual investigation of trace plots. The traces of all parameter estimates, or at least of those parameters with low ESS values should be visually inspected to assess MCMC stationarity. A good indicator of stationarity is when the trace plot has similarities to a "fuzzy caterpillar". 

Thus, both the calculation of ESS values as well as the visual inspection of trace plots should indicate stationarity of the MCMC chain; if this is not the case, the run should be resumed. For BEAST2 analyses, resuming a chain is possible with the "-resume" option when using BEAST2 on the command-line, or by selecting option "resume: appends log to existing files" in the drop-down menu at the top of the BEAST2 window when using the GUI version.

* Open files `FcC_supermatrix.log` and  `FcC_supermatrix2.log` in the program Tracer. The Tracer window should then look more or less as shown in the next screenshot<p align="center"><img src="images/tracer_1.png" alt="tracer" width="900"></p> In the top left part of the Tracer window, you'll see a list of the loaded log files. This part of the window also specifies the number of states found in this file, and the burn-in to be cut from the beginning of the MCMC chain.

	In the bottom left part of the Tracer window, you'll see statistics for the estimate of the posterior probability (just named "posterior"), the likelihood, and the prior probability (just named "prior"), as well as for the parameters estimated during the analysis (except the phylogeny, which also represents a set of parameters). The second column in this part shows the mean estimates for each parameter and their ESS values. 

	In the top right part of the Tracer window, you will see more detailed statistics for the parameter currently selected in the bottom left part of the window. Finally, in the bottom right, you will see a visualization of the samples taken during the MCMC search. By default, these are shown in the form of a histogram as in the above screenshot.

* With the posterior probability still being selected in the list at the bottom left, click on the tab for "Trace" (at the very top right). You will see how the posterior probability changed over the course of the MCMC. This trace plot should ideally have the form of a "fuzzy caterpillar", but as you can see from the next screenshot, this is not the case for the posterior probability.<p align="center"><img src="img/tracer2.png" alt="Tracer" width="700"></p>

* Now, click on the prior probability in the list at the bottom left of the window. You'll note that the trace looks very similar to that of the posterior, which may not be surprising given that the posterior probability is a (normalized) product of the prior probability and the likelihood. Thus, the auto-correlation in the prior probability seems to drive the auto-correlation in the posterior probability. Another way to visualize this is to select both the posterior and the prior probability at the same time (you may have to shift-click to do so) and then click on the "Joint-Marginal" tab next to the "Trace" tab. You'll see once again that the two measures are strongly correlated as in the next screenshot.<p align="center"><img src="img/tracer3.png" alt="Tracer" width="700"></p>



	
	



