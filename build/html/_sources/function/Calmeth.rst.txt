Calculate DNA methylation level
===============================

.. contents:: 
    :local:

Calmeth
-------

Calculate DNA methylation level from alignment files, you can obtained single-base cytosine DNA
methylation results, and the chromosome region DNA methylation levels files.

.. code:: bash

    An example usage is:
      with bam file:
        calmeth [options] -g genome.fa  -b alignment.sort.bam -m output.methrario.mbw
      with sam file:
        calmeth [options] -g genome.fa  -i alignment.sort.sam -m output.methrario.mbw

.. important:: The bam or sam file MUST sorted by `samtools sort`.


Paramaters
----------

+---------------------+--------------------------------------------------------------------------+
| **[ Main paramaters ]**                                                                        |
+=====================+==========================================================================+
| -m/--methratio      | [MethFileNamePrefix]  Predix of methratio output file (mbw)              |
+---------------------+--------------------------------------------------------------------------+
| --genome/-g         | Name of the genome mapped against, MUST build index first :doc:`bdindex` |
+---------------------+--------------------------------------------------------------------------+
| -i/--input          | Sam format file, sorted by samtools sort.                                |
+---------------------+--------------------------------------------------------------------------+
| -b/--binput         | Bam format file, sorted by samtools sort.                                |
+---------------------+--------------------------------------------------------------------------+
| -Q [int]            | caculate the methratio while read QulityScore >= Q. default:20           |
+---------------------+--------------------------------------------------------------------------+
| -n [float]          | Number of mismatches, default 0.06 percentage of read length. [0-1]      |
+---------------------+--------------------------------------------------------------------------+
| -c|--coverage       | >= <INT> coverage. default:4                                             |
+---------------------+--------------------------------------------------------------------------+
| -nC                 | >= <INT> Cs per region. default:1                                        |
+---------------------+--------------------------------------------------------------------------+
| -R/--Regions        | Bins for DMR caculate , default 1000(1kb) .                              |
+---------------------+--------------------------------------------------------------------------+
| --binsfile                                                                                     |
+----+-------------------------------------------------------------------------------------------+
|    |DNA methylation level distributions in chrosome, default output file: {Prefix}.methBins.txt|
+----+----------------+--------------------------------------------------------------------------+
| -s/--step                                                                                      |
+----+-------------------------------------------------------------------------------------------+
|    | Chrosome using an overlapping sliding window of 100000bp at a step of 50000bp.            |
|    | default step: 50000(bp)                                                                   |
+----+----------------+--------------------------------------------------------------------------+
| -r/--remove_dup     |  REMOVE_DUP, default:true                                                |
+----+----------------+--------------------------------------------------------------------------+
| --zl                | The maximum number of zoom levels. [1-10], default: 2                    |
+----+----------------+--------------------------------------------------------------------------+
| -as [0/1]           | If print calculated alignment reads in sam/bam file. default:0           |
+----+----------------+--------------------------------------------------------------------------+
| -f|--sam [outfile]                                                                             |
+----+-------------------------------------------------------------------------------------------+
|    | f for sam format outfile contain methState.                                               |
+----+----------------+--------------------------------------------------------------------------+
| --sam-seq-beforeBS  |  Converting BS read to the genome sequences.                             |
+---------------------+--------------------------------------------------------------------------+
| --help/-h           | Print help                                                               |
+---------------------+--------------------------------------------------------------------------+


Output files
------------

.. code:: bash

    1. prefix.methratio.mbw
    2. prefix.methBins.txt
    3. prefix_Region.CG/CHG/CHH.txt
    4. prefix.mCdensity.txt
    5. prefix.mCcatero.txt

Output file format
------------------

.. code:: bash

    1. methratio.mbw (binary file, view and processed with :doc:`BMtools` in BatMeth2)
        Chromosome Loci (end) methlevel CT_count Strand Context
        # ex. bmtools view -i test.mr.mbw -r Chr1:61-61
        # ex. Chr1    61      0.286364  11  +       CHH
        # CT_count     The number of coverage in this base pair.
        # BigWig for genome browser, suggest with end col.
    2. methBins
        Chrom BinIndex methlevel context
        # ex. Chr1    1       0.113674        CG
        # The BinIndex is defined by -s paramater in calmeth.
        # This file can be used for visualization the DNA methylation level acorss the chromosome.
    3. Region
        chrom regionStart strand context c_count ct_count
        # ex. Chr1    1001    +       CG      1       227
        # The bins methylation level output file (BS.mr_Region.C*.txt) can be used to do DMR detection.
    4. mCdensity
        CG/CHG/CHH C count in [0, 1%) [1%, 2%) ... [49%, 50%) ... [99%, 100%]
        # According to the DNA methylation level, the number of cytosine sites at different methylation levels was counted from 0 to 100.
    5. mCcatero
        Average DNA methylation level including mC, mCG and other states.


.. tip:: For feature requests or bug reports please open an issue `on github <http://github.com/ZhouQiangwei/BatMeth2>`__.
