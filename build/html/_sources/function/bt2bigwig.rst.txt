Meth2BigWig
===========

BatMeth2: An Integrated Package for Bisulfite DNA Methylation Data Analysis with Indel-sensitive Mapping.  

.. contents:: 
    :local:

methratio2bw
------------

* The methratio file calculated by calmeth, the format is `chrom pos strand context nC nCover methlevel`.
For exsample: `chr1    34      -       CHG     2       14      0.142857`

For bigWig with strand information

.. code:: bash

    python batmeth2_to_bigwig.py -sort -strand genome.fa.fai prefix.methratio.txt
    # genome.fa.fai can be prepared by `samtools faidx genome.fa`

or for bigWig without strand information

.. code:: bash

    python batmeth2_to_bigwig.py -sort genome.fa.fai prefix.methratio.txt

Run `BatMeth2` to see information on usage.

.. tip:: For feature requests or bug reports please open an issue `on github <http://github.com/ZhouQiangwei/BatMeth2>`__.
