.. BatMeth2 documentation master file, created by
   sphinx-quickstart on Thu Dec 10 21:24:25 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

BatMeth2: DNA Methylation Data Analysis
=======================================

.. image:: media/BatMeth2-pipeline.jpg

BatMeth2 is an **easy-to-use, auto-run** package for DNA methylation analyses. 
In order to complete the DNA methylation data analysis more conveniently, 
we packaged all the functions to complete an easy-to-use, auto-run package for DNA methylation analysis. 
During the execution of BatMeth2 Tool, an html report is generated about statistics of the sample.

We privide a binary indexed mbw format in this version, similar to BigWig but 
with coverage and context information. mbw format can be used for view and calculate 
DNA methylation level of anny chromsome region quickly. This file also can be used as 
BigWig file for genome browser visulization. Besides, mbw format file has smaller size 
than text format. Also, we provide a tool named bmtools for view and process mbw file. 
And we also provide bmDMR tool instead of batDMR for detect DMC and DMR more faster based on 
mbw input files. 

**Installation**

* Please download and install the tools (see :doc:`function/install`)

The functions you can use BatMeth2 to do:

* :doc:`function/Alignment`: Align bsseq data
* :doc:`function/Calmeth`: Calulate DNA methylation level (ML) across whole genome output mbw format.
* :doc:`function/BMtools`: tools for DNA methylation in mbw format, and prepare BigWig file for browser.
* :doc:`function/DiffMeth`: Perform differential analyses with auto defined regions or predefined regions. 
* :doc:`function/PlotMeth`: Plot DNA ML profile, heatmap or boxplot across genes/TEs/etc. 


Contents
--------
.. toctree::
   :maxdepth: 1

   function/install
   function/example
   function/bdindex
   function/Pipeline
   function/Alignment
   function/Calmeth
   function/BMtools
   function/PlotMeth
   function/DiffMeth
   function/Requirements
   
While developing BatMeth2, we continuously strive to create software
that fulfills the following criteria:

-  raw fastq reads quality control and **efficiently align bisulfite
   sequencing data**
-  **calculate DNA methylation level based on sorted BAM file** for single
   base or chromosome region and genes.
-  **new methlation mbw format with index** can calculate DNA methylation level
   quickly.
-  enable **customized down-stream analyses**, espacially with visulization
-  generation of **highly customizable images** (change colours, size,
   labels, file format, etc.)


Citation
^^^^^^^^

Please cite BatMeth2 as follows:

Zhou Q, Lim J-Q, Sung W-K, Li G: An integrated package for bisulfite DNA methylation data analysis with Indel-sensitive mapping. BMC Bioinformatics 2019, 20:47.
https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-018-2593-4



.. tip:: For feature requests or bug reports please open an issue `on github <http://github.com/ZhouQiangwei/BatMeth2-mbw>`__.

