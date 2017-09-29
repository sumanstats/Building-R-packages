=============
Data Packages
=============


There are several packages which were created for the sole purpose of distributing data including `janeaustenr <https://github.com/juliasilge/janeaustenr>`_, `gapminder <https://github.com/jennybc/gapminder>`_, `babynames <https://github.com/hadley/babynames>`_, and `lego <https://github.com/seankross/lego>`_. Using an R package as a means of distributing data has advantages and disadvantages. On one hand the data is extremely easy to load into R, a user only needs to install and load the package. This can be useful for teaching folks who are new to R and may not be familiar with importing and cleaning data. Data packages also allow you document datasets using ``roxygen2``, which provides a much cleaner and more programmer-friendly kind of code book compared to including a file that describes the data. On the other hand data in a data package is not accessible to people who are not using R, though there's nothing stopping you from distributing the data in multiple ways.

If you decide to create a data package you should document the process that you used to obtain, clean, and save the data. One approach to doing this is to use the ``use_data_raw()`` function from ``devtools``. This will create a directory inside of your package called ``data_raw``. Inside of this directory you should include any raw files that the data objects in you package are derived from. You should also include one or more R scripts which import, clean, and save those data objects in your R package. Theoretically if you needed to update the data package with new data files you should be able to just run these scripts again in order to rebuild your package.




Summary
*******

Including data in a package is useful for showing new users how to use your package, using data internally, and sharing and documenting datasets. The ``devtools`` package includes several useful functions to help you add data to your package including ``use_data()`` and ``use_data_raw()``. You can document data within your package just like you would document a function.
