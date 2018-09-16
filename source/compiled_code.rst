==================
src/ sub-directory
==================

The ``src`` sub-directory contains all of your C/C++ code, either in a single file, or 
in multiple files.

**************
Compiled code
**************


In many cases we may need to include compiled code in our R packages.
``Rcpp`` package is especially useful and more easy to learn to include ``C++`` code 
in our packages.

Other compiled languages can also be used: ``Rust, C and Fortran``.

For including ``Rust`` code in R, this project looks promising: `<https://rustr.org/>`_.
For more details see **Writing R Extensions:** `System and foreign language interfaces <https://cran.r-project.org/doc/manuals/r-release/R-exts.html#System-and-foreign-language-interfaces>`_.

R is weak in some kinds of operations. If you need operations listed below, 
it is time to consider using Rcpp (C++).

+ Loop operations.
+ Accessing each elements of a vector/matrix.
+ Recurrent function calls within loops.
+ Changing the size of vectors dynamically.
+ For advanced data structures and algorithms.


*************************
Building the setup (Linux)
*************************

^^^^^^^^^
Using GCC
^^^^^^^^^

To compile code in C++ in ``Linux``, install r-base-dev with this command 
in your Debian/Ubuntu:
``apt-get install r-base-dev``. This will pull gcc and g++ with openmp support to compile your C++ code.


.. _using-clang:

^^^^^^^^^^^^
Using Clang
^^^^^^^^^^^^

In terminal, install clang, libiomp-dev and ccache:

``apt-get install ccache clang libiomp-dev``.

Now create ``~/.R/Makevars`` file with:

``mkdir ~/.R/ && nano ~/.R/Makevars``

and fill it with:


.. code-block:: r

    CC=ccache clang -Qunused-arguments
    CXX=ccache clang++ -Qunused-arguments
    CCACHE_CPP2=yes

After this your are ready to compile with clang. 

.. note::

    Use clang instead of gcc to compile your C++ code: it gives much better error messages. 
    You can make clang the default by creating a ~/.R/Makevars (linux and mac) as shown above.



******************
Test your setup
******************

In your Linux box in terminal, type ``R`` to get R console and type:

.. code-block:: r
    :linenos:
    
    install.packages("data.table")

If it installs without any error, your setup for ``Linux`` is ready to experiment
with compiled code in C/C++.

For details on including **C++** code, read `Rewriting R code in C++ <https://adv-r.hadley.nz/rcpp.html>`_ chapter from Hadley's **Advanced R** book.
