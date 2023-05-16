# Gen-711-Final-Project
Analysis of Cyanobacteria in New England lakes

# Authors
Dominic Carignan
and
Colby Griffin
# Background

Cyanobacterial blooms are becoming more common in lakes and when they occur, there are numerous probems they can pose to humans and other animals in the surroudnng ecosystems. These bacteria are known to produce sedondary metabolites that are toxic to humans and other animals in large quantities like microsystin, saxitoxins, and nodularins. In addition to this, cyanobacteria heavily contribute to the eutrophication of lakes, which is the process when a lake loses much of its dissovled oxygen content due to algal and cyanobacterial blooms covering the surface. This process ends up killing most of the life below the surface as the water becomes toxic and incapapble of supporting life, leaving behind a dead zone that can be toxic to the surrounding wildlife. Surveying lakes for their cyanobacterial contents could help further understand which bacteria contribute the most to blooms and how to limit them and their effects on the surroudning life.

We were interested in the cyanobacteria research conducted by Valdez-Cano et al 2022 on North Atlatnic lakes. The research centers around using metagenomic approaches to identify which cyanbacteria are present in the serveyed lakes, as well as assesing their potential to produce toxins. PCR based methods were used in order to amplify well known toxin producing genes from different bacteria in the sample. The lakes were surveyed thorughout the year to see how bacterial compisition changed. We compared a set of data collected from New england lakes over a span of a year to a metadata set in order to observe how the bacterial compitisions change over time.

# Methods

We downloaded our sequences from /tmp/gen711_project_data/cyano/fastqs using the ron supercomputer and the data was in fastqz format

First we trimmed off the poly g tail from the reads which are commonly found on nova-seq data, using a fastp script which required an input of the poly g cutoff length, which reads to trim, and an output directory to store the trimmed reads in. 

We ran the rest of analysis of the poly g trimmed data using the qiime 2022.8 program loaded on the conda environement. 

First we put our reads into a qiime file using the "qiime tools import" command to condense the fastq files inot one .qza file to run the rest of the commands on.

To further trim the sequences, we used cutadapt in qiime to remove the primer sequences from all the reeads in the .qza file. To visualize this file we then ran "demux summarize" command to make a summary.qza file that is viewable and human readable.

*These viewable files can be found in the output folder*

The next step is to denoise the data using "dada2 denoise-paired" in qiime which is a program that will use the eroror rate and base call quality of the data then try to correct the errors in it. This also gives us an output with all ASV's that can be viewed in multiple human readable formats after exporting out of the .qza format

After this a taxonomical comaprison was done between our data and a refrence data base to identify the species present in our dataset. Using "qiime feature-classifier classify-sklearn" and "qiime taxa barplot" we were able to create a graph displaying all concentrations of organsims present in each sample.

for further analysis and plot generation for the data, more commands were used in the qiime environment in order to create a core-metrics folder with "qiime phylogeny align-to-tree-mafft-fasttree" and "qiime phylogeny align-to-tree-mafft-fasttree" with an output folder of core-metrics. 

Once this folder is made, a multitude of plots can be made with the data in qiime, the ones we used were from "qiime diversity alpha-group-significance" and "qiime emperor biplot" commands which generated a barplot and PCA plot respictvelty. Each plot was mad ebby using the trimmed rreads from our data and comparing them to a metadataset. 

*The real code for any command in this section can be found in the "Final Project Code" file*

# Findings

![Screenshot (5)](https://github.com/cmg1126/Gen-711-Final-Project/assets/130592752/324c7c7a-540b-4c6f-8785-e061a931729f)

We obtained this plot from running qiime diversity "alpha-group-significance" on the core metrics folder which comapred the reads from our data to a set of metadata. This plot represents the how the bacterial community changed based on collection date. 

![emperor.png](https://github.com/cmg1126/Gen-711-Final-Project/blob/main/emperor.png)

We obtained this plot from running "qiime emporer bipolot" on the core metrics folder which comapred the reads from our data to a metadata set. This is a PCA of bacterial communites, each color represents a different month during the summer. 

![Screenshot (6)](https://github.com/cmg1126/Gen-711-Final-Project/assets/130592752/e06140aa-29f2-4dc3-a52b-5c798bf01f4c)

We obtained this plot by running "qiime taxa barplot" on our trimmed reads and compared them to a metadatset to indentify the taxa in our sample. This is a barplot of the bacterial composition in the samples, most notably purple is cyanobacteria. 
