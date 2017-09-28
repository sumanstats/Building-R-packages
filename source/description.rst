================
DESCRIPTION file
================

The DESCRIPTION file is an essential part of an R package because it contains key metadata for the package that is used by repositories like CRAN and by R itself. In particular, this file contains the package name, the version number, the author and maintainer contact information, the license information, as well as any dependencies on other packages.

As an example, here is the DESCRIPTION file for the mvtsplot package on CRAN. This package provides a function for plotting multivariate time series data.

.. code-block:: r
    :linenos:

    Package:  mvtsplot
    Version:  1.0-3
    Date:  2016-05-13
    Depends:  R (>= 3.0.0)
    Imports: splines, graphics, grDevices, stats, RColorBrewer
    Title:  Multivariate Time Series Plot
    Author:  Roger D. Peng <rpeng@jhsph.edu>
    Maintainer:  Roger D. Peng <rpeng@jhsph.edu>
    Description:  A function for plotting multivariate time series data.
    License:  GPL (>= 2)
    URL: https://github.com/rdpeng/mvtsplot


