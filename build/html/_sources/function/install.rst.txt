Installation
=============

BatMeth2: An Integrated Package for Bisulfite DNA Methylation Data Analysis with Indel-sensitive Mapping.  

.. contents:: 
    :local:

Requirements
-------------

* gcc >= v4.8 
* :doc:`gsl`
* :doc:`zlib`
* samtools >= v1.3.1 
* `fastp, raw reads as input need <https://github.com/OpenGene/fastp>`_.

The details of requirements can see :doc:`Requirements`

Install
-------
.. code:: bash

    a) git clone https://github.com/ZhouQiangwei/BatMeth2.git
    b) Change directory into the top directory of BatMeth2
	$ cd BatMeth2
    c) Type 
	$ ./configure
	$ make
	$ make install
    e) The binary of BatMeth2 will be created in bin/

.. tip:: For feature requests or bug reports please open an issue `on github <http://github.com/ZhouQiangwei/BatMeth2>`__.
