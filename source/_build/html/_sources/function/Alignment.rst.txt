Alignment
=========

.. contents:: 
    :local:

BatMeth2  align
---------------

Single-end-reads
^^^^^^^^^^^^^^^^

DNA methylation sequencing single-end data alignment:

.. code:: bash

    An example usage is:
        batmeth2 -g /data/index/genome/genome.fa -i Read.fq.gz -o outPrefix -p 10

Paired-end-reads
^^^^^^^^^^^^^^^^

DNA methylation sequencing paired-end data alignment:

.. code:: bash

    An example usage is:
        batmeth2 -g /data/index/genome/genome.fa -i Read_R1_left.fq.gz -i Read_R2_right.fq.gz\
        -o outPrefix -p 10

Parameters
^^^^^^^^^^ 

+---------------------+--------------------------------------------------------------------------+
| **[ Main paramaters ]**                                                                        |
+=====================+==========================================================================+
| --inputfile/-i      | bs-seq input fastq files, fastq format or gzip format                    |
+---------------------+--------------------------------------------------------------------------+
| --genome/-g         | Name of the genome mapped against, MUST build index first :doc:`bdindex` |
+---------------------+--------------------------------------------------------------------------+
| --outputfile/-o     | Name of output file prefix                                               |
+---------------------+--------------------------------------------------------------------------+
| --threads/-p        | Launch <integer> threads                                                 |
+---------------------+--------------------------------------------------------------------------+
| --non_directional   | Alignments to all four bisulfite strands will be reported. Default: OFF. |
+---------------------+--------------------------------------------------------------------------+
| --insertsize/-s     | inital insert size, default 600, will be aoto detected by input files    |
+---------------------+--------------------------------------------------------------------------+
| --std/-d            | standard deviatiion of reads distribution, will aoto detected by input   |
+---------------------+--------------------------------------------------------------------------+
| --flanksize/-f      | size of flanking region for Smith-Waterman                               |
+---------------------+--------------------------------------------------------------------------+
| --swlimit           | try at most <integer> sw extensions                                      |
+---------------------+--------------------------------------------------------------------------+
| --indelsize         | indel size                                                               |
+---------------------+--------------------------------------------------------------------------+
| --NoInDels/-I       | not to find the indels result                                            |
+---------------------+--------------------------------------------------------------------------+
| --help/-h           | Print help                                                               |
+---------------------+--------------------------------------------------------------------------+

Note: To use BatMeth2, you need to first index the genome with :doc:`bdindex`.

.. tip:: For feature requests or bug reports please open an issue `on github <http://github.com/ZhouQiangwei/BatMeth2>`__.
