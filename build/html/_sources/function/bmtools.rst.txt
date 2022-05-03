bmtools
=======

.. contents:: 
    :local:

BatMeth2 bmtools view for mbw
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can view and process mbw file with bmtools:

.. code:: bash

    $ bmtools view -i mutant.methratio.mbw | head
    
obtained text format methylation results


Main functions
^^^^^^^^^^^^^^

+---------------------+--------------------------------------------------------------------------+
| **[ Main paramaters ]**                                                                        |
+=====================+==========================================================================+
|                     | bmtools <mode> [opnions]                                                 |
+---------------------+--------------------------------------------------------------------------+
|Usage:               |                                                                          |
+---------------------+--------------------------------------------------------------------------+
| [mode]              | mr2mbw view overlap regionstats bodystats profile chromstats             |
+---------------------+--------------------------------------------------------------------------+
| mr2mbw              | convert txt meth file to mbw format                                      |
+---------------------+--------------------------------------------------------------------------+
| view                | mbw format to txt meth                                                   |
+---------------------+--------------------------------------------------------------------------+
| overlap             | overlap cytosine site with more than two mbw files                       |
+---------------------+--------------------------------------------------------------------------+
| regionstats         | calculate DNA methylation level of per region                            |
+---------------------+--------------------------------------------------------------------------+
| bodystats           | calculate DNA methylation level of body, upstream and downstream.        |
+---------------------+--------------------------------------------------------------------------+
| profile             | calculate DNA methylation profile                                        |
+---------------------+--------------------------------------------------------------------------+
| chromstats          | calculate DNA methylation level across chromosome                        |
+---------------------+--------------------------------------------------------------------------+
| -h|--help                                                                                      |
+---------------------+--------------------------------------------------------------------------+


bmtools mr2mbw
--------------

Convert methratio txt file to mbw binary file:

.. code:: bash

    $ bmtools mr2mbw -g genome.fa.size -m mutant.methratio.txt --outmbw mutant.methratio.mbw
    
obtained mbw format methylation results, you can see more details with 'bmtools mr2mbw -h'

bmtools view
------------

You can view and process mbw file with bmtools:

.. code:: bash

    $ bmtools view -i mutant.methratio.mbw | head
    
obtained text format methylation results

bmtools overlap
---------------

Overlap cytosine site with more than two mbw files:

.. code:: bash

    $ bmtools overlap -i sample1.methratio.mbw -i2 sample2.methratio.mbw

Or just with --bmfiles:

.. code:: bash

    $ bmtools overlap --bmfiles sample1.methratio.mbw sample2.methratio.mbw


bmtools regionstats
-------------------

Calculate DNA methylation level of chromosome region, genes, or TEs:

.. code:: bash

    $ bmtools regionstats -i sample1.methratio.mbw --gtf gene.gtf -o gene.meth.txt

Or with bed file:

.. code:: bash

    $ bmtools regionstats -i sample1.methratio.mbw --bed gene.bed -o gene.meth.txt

Or just calculate DNA methylation level of same regions:

.. code:: bash

    $ bmtools regionstats -i sample1.methratio.mbw -r chr1:1-2900;chr2:1-200,+ \
      -o gene.meth.txt

Please see 'bmtools regionstats' for more details.


bmtools bodystats
-----------------

Calculate DNA methylation level of gene body, upstream and downstream:

.. code:: bash

    $ bmtools bodystats -i sample1.methratio.mbw --gtf gene.gtf -o gene.meth.txt

Or with bed file:

.. code:: bash

    $ bmtools bodystats -i sample1.methratio.mbw --bed gene.bed -o gene.meth.txt

Or just calculate DNA methylation level of same regions:

.. code:: bash

    $ bmtools bodystats -i sample1.methratio.mbw -r chr1:1-2900;chr2:1-200,+ \
      -o gene.meth.txt

Please see 'bmtools bodystats' for more details.


bmtools profile
---------------

Calculate DNA methylation profile matrix and avarage matrix across gene body, upstream and downstream:

.. code:: bash

    $ bmtools profile -i sample1.methratio.mbw --gtf gene.gtf -o gene.profile \
      --regionextend 2000 --bodyX 1 --matrixX 5

Or with bed file:

.. code:: bash

    $ bmtools profile -i sample1.methratio.mbw --bed gene.bed -o gene.profile \
      --regionextend 2000 --bodyX 1 --matrixX 5

Please see 'bmtools profile' for more details.


bmtools chromstats
------------------

Calculate DNA methylation level across chromosome:

.. code:: bash

    $ bmtools chromstats -i sample1.methratio.mbw -o chromosome.meth.txt \
      --chromstep 100000 --stepmove 50000 --fstrand 3 --context 4

Please see 'bmtools chromstats' for more details.

.. tip:: For feature requests or bug reports please open an issue `on github <http://github.com/ZhouQiangwei/BatMeth2>`__.
