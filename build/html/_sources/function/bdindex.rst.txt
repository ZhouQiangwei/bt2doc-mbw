Build index
===========

BatMeth2: An Integrated Package for Bisulfite DNA Methylation Data Analysis with Indel-sensitive Mapping.  

.. contents:: 
    :local:

Genome index
------------

* Have a fasta-formatted reference file ready, and then make the neccessary pairing data-structure based on FM-index.

For WGBS type 

.. code:: bash

    BatMeth2 build_index GENOME.fa

or for RRBS 

.. code:: bash

    BatMeth2 build_index rrbs GENOME.fa

Run `BatMeth2` to see information on usage.


.. tip:: For feature requests or bug reports please open an issue `on github <http://github.com/ZhouQiangwei/BatMeth2>`__.
