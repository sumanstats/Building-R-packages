==============
Including Data
==============



Data Objects
************

Including data in your package is easy thanks to the devtools package. To include datasets in a package, first create the objects that you would like to include in your package inside of the global environment. You can include any R object in a package, not just data frames. Then make sure you're in your package directory and use the ``use_data()`` function, listing each object that you want to include in your package. The names of the objects that you pass as arguments to ``use_data()`` will be the names of the objects when a user loads the package, so make sure you like the variable names that you're using.

You should then document each data object that you're including in the package. This way package users can use common R help syntax like ``?dataset`` to find out more information about the included data set. You should create one R file called ``data.R`` in the R/ directory of your package. You can write the data documentation in the ``data.R`` file. Let's take a look at some documentation examples from the minimap package. First we'll look at the documentation for a data frame called maple:

.. code-block:: r
    :linenos:
    
    #' Production and farm value of maple products in Canada
    #'
    #' @source Statistics Canada. Table 001-0008 - Production and farm value of
    #'  maple products, annual. \url{http://www5.statcan.gc.ca/cansim/}
    #' @format A data frame with columns:
    #' \describe{
    #'  \item{Year}{A value between 1924 and 2015.}
    #'  \item{Syrup}{Maple products expressed as syrup, total in thousands of gallons.}
    #'  \item{CAD}{Gross value of maple products in thousands of Canadian dollars.}
    #'  \item{Region}{Postal code abbreviation for territory or province.}
    #' }
    #' @examples
    #' \dontrun{
    #'  maple
    #' }
    "maple"
    
Data frames that you include in your package should follow the general schema above where the documentation page has the following attributes:

- An informative title describing the object.

- A ``@source`` tag describing where the data was found.

- A ``@format`` tag which describes the data in each column of the data frame.

- And then finally a string with the name of the object.

The minimap package also includes a few vectors. Let's look at the documentation for ``mexico_abb``:

.. code-block:: r
    :linenos:
    
    #' Postal Abbreviations for Mexico
    #'
    #' @examples
    #' \dontrun{
    #'  mexico_abb
    #' }
    "mexico_abb"
    
You should always include a title for a description of a vector or any other object. If you need to elaborate on the details of a vector you can include a description in the documentation or a ``@source`` tag. Just like with data frames the documentation for a vector should end with a **string containing the name of the object**.

Raw Data
********

A common task for R packages is to take raw data from files and to import them into R objects so that they can be analyzed. You might want to include some sample raw data files so you can show different methods and options for importing the data. To include raw data files in your package you should create a directory under ``inst/extdata`` in your R package. If you stored a data file in this directory called ``response.json`` in ``inst/extdata`` and your package is named mypackage then a user could access the path to this file with ``system.file("extdata", "response.json", package = "mypackage")``. Include that line of code in the documentation to your package so that your users know how to access the raw data file.




Internal Data
*************

Functions in your package may need to have access to data that you don't want your users to be able to access. For example the **swirl** package contains translations for menu items into languages other than English, however that data has nothing to do with the purpose of the swirl package and so it's hidden from the user. To add internal data to your package you can use the ``use_data()`` function from devtools, however you must specify the ``internal = TRUE`` argument. All of the objects you pass to ``use_data(..., internal = TRUE)`` can be referenced by the same name within your R package. All of these objects will be saved to one file called ``R/sysdata.rda``.

