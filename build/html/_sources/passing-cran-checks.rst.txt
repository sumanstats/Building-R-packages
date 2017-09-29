===========
CRAN checks
===========


Before submitting a package to CRAN, you must pass a battery of tests that are run by the R itself via the R CMD check program. In RStudio, if you are in an R Package "Project" you can run R CMD check by clicking the Check button in the build tab. This will run a series of tests that check the metadata in your package, the NAMESPACE file, the code, the documentation, run any tests, build any vignettes, and many others.

Here is an example of the output form R CMD check for the filehash package which currently passes all tests.


.. code-block:: r
    :linenos:

    * using R version 3.3.2 (2016-10-31)
    * using platform: x86_64-apple-darwin13.4.0 (64-bit)
    * using session charset: UTF-8
    * checking for file 'filehash/DESCRIPTION' ... OK
    * this is package 'filehash' version '2.3'
    * checking package namespace information ... OK
    * checking package dependencies ... OK
    * checking if this is a source package ... OK
    * checking if there is a namespace ... OK
    * checking for executable files ... OK
    * checking for hidden files and directories ... OK
    * checking for portable file names ... OK
    * checking for sufficient/correct file permissions ... OK
    * checking whether package 'filehash' can be installed ... OK
    * checking installed package size ... OK
    * checking package directory ... OK
    * checking 'build' directory ... OK
    * checking DESCRIPTION meta-information ... OK
    * checking top-level files ... OK
    * checking for left-over files ... OK
    * checking index information ... OK
    * checking package subdirectories ... OK
    * checking R files for non-ASCII characters ... OK
    * checking R files for syntax errors ... OK
    * checking whether the package can be loaded ... OK
    * checking whether the package can be loaded with stated dependencies ... OK
    * checking whether the package can be unloaded cleanly ... OK
    * checking whether the namespace can be loaded with stated dependencies ... OK
    * checking whether the namespace can be unloaded cleanly ... OK
    * checking loading without being on the library search path ... OK
    * checking dependencies in R code ... OK
    * checking S3 generic/method consistency ... OK
    * checking replacement functions ... OK
    * checking foreign function calls ... OK
    * checking R code for possible problems ... OK
    * checking Rd files ... OK
    * checking Rd metadata ... OK
    * checking Rd cross-references ... OK
    * checking for missing documentation entries ... OK
    * checking for code/documentation mismatches ... OK
    * checking Rd \usage sections ... OK
    * checking Rd contents ... OK
    * checking for unstated dependencies in examples ... OK
    * checking line endings in C/C++/Fortran sources/headers ... OK
    * checking compiled code ... OK
    * checking sizes of PDF files under 'inst/doc' ... OK
    * checking installed files from 'inst/doc' ... OK
    * checking files in 'vignettes' ... OK
    * checking examples ... OK
    * checking for unstated dependencies in 'tests' ... OK
    * checking tests ...
     OK
    * checking for unstated dependencies in vignettes ... OK
    * checking package vignettes in 'inst/doc' ... OK
    * checking running R code from vignettes ...
       'filehash.Rnw' ... OK
     OK
    * checking re-building of vignette outputs ... OK
    * checking PDF version of manual ... OK
    * DONE
    Status: OK

Here is an example from the mvtsplot package where we've deliberately introduced some problems to the package in order to show the check output. Checks that have passed are not shown below.


.. code-block:: r
    :linenos:

    * checking foreign function calls ... OK
    * checking R code for possible problems ... NOTE
    drawImage: no visible global function definition for 'Axis'
    drawImageMargin: no visible global function definition for 'lm'
    drawImageMargin: no visible global function definition for 'Axis'
    splineFillIn: no visible global function definition for 'lm'
    Undefined global functions or variables:
      Axis lm
    Consider adding
      importFrom("graphics", "Axis")
      importFrom("stats", "lm")
    to your NAMESPACE file.

Here, it appears that the functions ``Axis()`` and ``lm()`` are needed by the package but are not available because they are not imported from their respective packages. In this case, R CMD check provides a suggestion of how you can modify the NAMESPACE package, but you are probably better off modifying the roxygen2 documentation in the code file instead.

Moving on the rest of the checks, we see:


.. code-block:: r
    :linenos:

    * checking for missing documentation entries ... OK
    * checking for code/documentation mismatches ... WARNING
    Codoc mismatches from documentation object 'mvtsplot':
    mvtsplot
      Code: function(x, group = NULL, xtime = NULL, norm = c("internal",
                     "global"), levels = 3, smooth.df = NULL, margin =
                     TRUE, sort = NULL, main = "", palette = "PRGn",
                     rowstat = "median", xlim, bottom.ylim = NULL,
                     right.xlim = NULL, gcol = 1)
      Docs: function(y, group = NULL, xtime = NULL, norm = c("internal",
                     "global"), levels = 3, smooth.df = NULL, margin =
                     TRUE, sort = NULL, main = "", palette = "PRGn",
                     rowstat = "median", xlim, bottom.ylim = NULL,
                     right.xlim = NULL, gcol = 1)
      Argument names in code not in docs:
        x
      Argument names in docs not in code:
        y
      Mismatches in argument names:
        Position: 1 Code: x Docs: y

Here the problem is that the code has the first argument named x while the documentation has the first argument named y.



.. code-block:: r
    :linenos:

    * checking Rd \usage sections ... WARNING
    Undocumented arguments in documentation object 'mvtsplot'
      'y'
    Documented arguments not in \usage in documentation object 'mvtsplot':
      'x'

    Functions with \usage entries need to have the appropriate \alias
    entries, and all their arguments documented.
    The \usage entries must correspond to syntactically valid R code.
    See chapter 'Writing R documentation files' in the 'Writing R
    Extensions' manual.


Because of the mismatch in code and documentation for the first argument, we have an argument that is not properly documented (y) and an argument that is documented but not used (x).

In case the checks fly by too quickly, you will receive a summary message the end saying what errors and warnings you got.



.. code-block:: r
    :linenos:

    * DONE
    Status: 2 WARNINGs, 1 NOTE
    

