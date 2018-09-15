================
Before You Start
================


Building R packages requires a toolchain that must be in place before you begin developing. If you are developing packages that contain only R code, then the tools you need come with R and RStudio. However, if you want to build packages with compiled C or Fortran code (or which to build other people's packages with such code), then you will need to install additional tools. Which tools you install depends on what platform you are running.


Making the Build Chain
----------------------

Windows
*******

On Windows, the R Core has put together a package of tools that you can download all at once and install via a simple installer tool. The `Rtools <https://cran.r-project.org/bin/windows/Rtools/>`_ package comes in different versions, depending on the version of R that you are using. Make sure to get the version of Rtools that matches your version of R. Once you have installed this, you will have most of the tools needed to build R packages. You can optionally install a few other tools, documented `here <https://cran.r-project.org/bin/windows/Rtools/Rtools.txt>`_.


Linux
*****

If you are using R on a Unix-like system then you may have already have the tools for building R packages. In particular, if you built R from the sources, then you already have a C compiler and Fortran compiler. 
In ``Debian``, ``apt-get install build-essential`` will install the necessary build tools like ``gcc``, ``g++``, ``make`` and many others.

If, however, you installed R from a package management system, then you may need to install the compilers, as well as the **header files**. These usually coming in packages with the suffix **-devel**. For example, the header files for the readline package may come in the package ``readline-devel``. The catch is that these **-devel** packages are not needed to run R, only to build R packages from the sources.
For using ``clang`` instead of ``gcc`` for package building, see :ref:`using-clang`.
