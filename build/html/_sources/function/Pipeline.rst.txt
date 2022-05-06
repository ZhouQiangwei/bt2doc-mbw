Pipeline
========

.. tip:: BatMeth2 can perform one click analysis or the following modules step by step:

    * :doc:`Alignment`
    * :doc:`Calmeth` 
    * :doc:`MethyGff`
    * :doc:`bt2bigwig`
    * :doc:`PlotMeth`
    * :doc:`DiffMeth`

.. contents:: 
    :local:

+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+
| tool                    | input files                        | main output file(s)              | main application                                                       |
+=========================+====================================+==================================+========================================================================+
|:doc:`Alignment`         | Single/Paired-end fastq/gz files   | alignment sam/bam file           | Perform DNA methylation level calculation and SNP/ASM detection        |
+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+
|:doc:`Calmeth`           | BS-seq align sorted sam/bam file   | methratio file (loci/region)     | Perform DNA methylation visulization on chromosome, and diff analysis  |
+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+
|:doc:`MethyGff`          | methration file from calmeth       | methlevel file on genes/TEs etc. | DNA methylation profile or heatmap on genes/TEs/peak regions/etc.      |
+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+
|:doc:`bt2bigwig`         | methration file from calmeth       | bigwig files (c/cg/chg/chh)      | Convert DNA methylation file to bigwig format.                         |
+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+
|:doc:`PlotMeth`          | methy files from calmeth/methyGff  | methy profile/heatmap/boxplot    | visulization of DNA methylation across samples                         |
+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+
|:doc:`DiffMeth`          | methration file from calmeth       | Diff methy cytosines/regions     | Perform Differential DNA methylation analysis                          |
+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+


BatMeth2 pipeline
^^^^^^^^^^^^^^^^^

An easy-to-use, auto-run package for DNA methylation analyses:

Raw reads:

.. code:: bash

    BatMeth2 pipel --fastp ~/location/to/fastp \
    -1 Raw_reads_1.fq.gz -2 Raw_read_2.fq.gz \
    -g ./batmeth2index/genome.fa \
    -o meth -p 8 --gff ./gene.gff

Or clean reads:

.. code:: bash

    BatMeth2 pipel -1 Clean_reads_1.fq.gz -2 Clean_read_2.fq.gz \
    -g ./batmeth2index/genome.fa \
    -o meth -p 8 --gff ./gene.gff


You can always see all available command-line options via --help:

.. code:: bash

    $ BatMeth2 --help

- After the program runs successfully, a series of files with '- o' as prefix and DNA methylation level will be generated in the output directory. Please refer to the doc for the specific output file and format details. 
- In addition, there will be an HTML report file containing basic information and statistical results of data analysis.

BatMeth2 pipeline main parameters
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Build index
"""""""""""

Usage:  (must run this step first) 

1. Build index using for wgbs data

.. code:: bash

    $ BatMeth2 build_index genomefile

2. Build index using for rrbs data

.. code:: bash

    $ BatMeth2 build_index rrbs genomefile 

Main Alignment paramaters
"""""""""""""""""""""""""

+---------------------+--------------------------------------------------------------------------+
| **[ Fastq Quality Conreol ]**                                                                  |
+---------------------+--------------------------------------------------------------------------+
| --fastp             | fastp program location                                                   |
+---------------------+--------------------------------------------------------------------------+
| If --fastp is not defined, the input file should be clean data.                                |
+---------------------+--------------------------------------------------------------------------+
| **[ Main paramaters ]**                                                                        |
+---------------------+--------------------------------------------------------------------------+
| -o                  | Name of output file prefix                                               |
+---------------------+--------------------------------------------------------------------------+
| -O                                                                                             |
+----+-------------------------------------------------------------------------------------------+
|    | Output of result file to specified folder, default output to current folder (./)          |
+----+-------------------------------------------------------------------------------------------+
| **[ Aligners paramaters ]**                                                                    |
+---------------------+--------------------------------------------------------------------------+
| -g                  | Name of the genome mapped against                                        |
+---------------------+--------------------------------------------------------------------------+
| -i                                                                                             |
+----+-------------------------------------------------------------------------------------------+
|    | Name of input file, if paired-end. please use -1, -2,                                     |
|    | input files can be separated by commas. eg. -1 readA.fq.gz,readB.fq.gz -2 ..              |
+----+----------------+--------------------------------------------------------------------------+
| -1                  | Name of input file left end, if single-end. please use -i                |
+---------------------+--------------------------------------------------------------------------+
| -2                  | Name of input file left end                                              |
+---------------------+--------------------------------------------------------------------------+
| -p                  |  Launch <integer> threads                                                |
+---------------------+--------------------------------------------------------------------------+
| -n                  | maximum mismatches allowed due to seq. errors [0-1]                      |
+---------------------+--------------------------------------------------------------------------+
| **[ Select aligner ]**                                                                         |
+---------------------+--------------------------------------------------------------------------+
| --aligner                                                                                      |
+----+-------------------------------------------------------------------------------------------+
|    | BatMeth2(default), bwa-meth, bsmap, bismark2,                                             |
|    | no (exit output_prefix.sam file, no need align again)                                     |
+----+-------------------------------------------------------------------------------------------+
| --go (When aligner not BatMeth2)                                                               |
+----+-------------------------------------------------------------------------------------------+
|    | Name of the genome, contaion index build by aligner. (bwa-meth/bismark2)                  |
+----+-------------------------------------------------------------------------------------------+
    
Calmeth paramaters
""""""""""""""""""      

+---------------------+--------------------------------------------------------------------------+
| --Qual              | calculate the methratio while read QulityScore >= Q. default:20          |
+---------------------+--------------------------------------------------------------------------+
| --redup             | REMOVE_DUP, 0 or 1, default 1                                            |
+---------------------+--------------------------------------------------------------------------+
| --region            | Bins for region meth calculate , default 1000bp.                         |
+---------------------+--------------------------------------------------------------------------+
| -f                                                                                             |
+-----+---------------+--------------------------------------------------------------------------+
|     | for sam format outfile contain methState. [0 or 1], default: 0 (dont output this file).  |
+-----+---------------+--------------------------------------------------------------------------+
| --coverage          | >= <INT> coverage. default: 4                                            |
+---------------------+--------------------------------------------------------------------------+
| --binCover          | >= <INT> nCs per region. default: 3                                      |
+---------------------+--------------------------------------------------------------------------+
| --chromstep         | >= <INT> nCs per region. default: 3                                      |
+-----+---------------+--------------------------------------------------------------------------+
|     | Chromosome using an overlapping sliding window of 100000bp at a step of 50000bp\         | 
|     | default step: 50000(bp)                                                                  |
+-----+------------------------------------------------------------------------------------------+

MethyGff/Annoation paramaters
"""""""""""""""""""""""""""""

+---------------------+--------------------------------------------------------------------------+
| --gtf/--gff/--bed/--bed4/--bed5                                                                |
+----+-------------------------------------------------------------------------------------------+
|    | gtf / gff / bed files, bed: Chr start end; bed4: Chr start end strand; \                  |
|    | bed5: Chr start end id strand;                                                            |
+----+-------------------------------------------------------------------------------------------+
| -d/--distance                                                                                  |
+----+-------------------------------------------------------------------------------------------+
|    | DNA methylation level distributions in body and <INT>-bp flanking sequences. \            |
|    | The distance of upstream and downstream. default:2000                                     |
+----+-------------------------------------------------------------------------------------------+
| --step                                                                                         |
+----+-------------------------------------------------------------------------------------------+
|    | Gene body and their flanking sequences using an overlapping sliding window of 5%\         |
|    | of the sequence length at a step of 2.5% of the sequence length. So default \             |
|    | step: 0.025 (2.5%)                                                                        |
+----+----------------+--------------------------------------------------------------------------+
| -C                  | <= <INT> coverage. default:1000                                          |
+---------------------+--------------------------------------------------------------------------+
| -bl/--bodyLen       | Body length to which all regions will be fit. (default: same as -d)      |
+---------------------+--------------------------------------------------------------------------+


Output files
^^^^^^^^^^^^

Output file format and details see "https://github.com/GuoliangLi-HZAU/BatMeth2/blob/master/output_details.pdf".<br>

Output report details see "https://www.dna-asmdb.com/download/batmeth2.html" .<br>

.. tip:: For feature requests or bug reports please open an issue `on github <http://github.com/ZhouQiangwei/BatMeth2>`__.
