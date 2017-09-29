=======================
roxygen2 and help files
=======================


In addition to writing tutorials that give an overview of your whole package, you should also write specific documentation showing users how to use and interpret any functions you expect users to directly call.

These help files will ultimately go in a folder called /man of your package, in an R documentation format (``.Rd`` file extensions) that is fairly similar to LaTex. You used to have to write all of these files as separate files. However, the ``roxygen2`` package lets you put all of the help information directly in the code where you define each function.

With ``roxygen2``, you add the help file information directly above the code where you define each functions, in the R scripts saved in the R subdirectory of the package directory. You start each line of the ``roxygen2`` documentation with # ' (the second character is an apostrophe, not a backtick).

The **first line** of the documentation should give a short title for the function, and the **next block** of documentation should be a longer description. After that, you will use tags that start with ``@`` to define each element you're including. You should **leave an empty line** between each section of documentation, and you can use indentation for second and later lines of elements to make the code easier to read.

Here is a basic example of how this ``roxygen2`` documentation would look for a simple "Hello world" function:

.. code-block:: r
    :linenos:
    
    #' Print "Hello world" 
    #'
    #' This is a simple function that, by default, prints "Hello world". You can 
    #' customize the text to print (using the \code{to_print} argument) and add
    #' an exclamation point (\code{excited = TRUE}).
    #'
    #' @param to_print A character string giving the text the function will print
    #' @param excited Logical value specifying whether to include an exclamation
    #'    point after the text
    #' 
    #' @return This function returns a phrase to print, with or without an 
    #'    exclamation point added. As a side effect, this function also prints out
    #'    the phrase. 
    #'
    #' @examples
    #' hello_world()
    #' hello_world(excited = TRUE)
    #' hello_world(to_print = "Hi world")
    #'
    #' @export
    hello_world <- function(to_print = "Hello world", excited = FALSE){
        if(excited) to_print <- paste0(to_print, "!")
        print(to_print)
    }
    
    
Common roxygen2 tags 
********************

Here are some of the common roxygen2 tags to use in creating this documentation: `Table of common roxygen2 tags <https://bookdown.org/rdpeng/RProgDA/documentation.html#common-roxygen2-tags>`_.

Here are a few things to keep in mind when writing help files using roxygen2:

The tags ``@example`` and ``@examples`` do different things. You should always use the ``@examples`` **(plural)** tag for example code, or you will get errors when you build the documentation.

The ``@inheritParams`` function can save you a lot of time, because if you are using the same parameters in multiple functions in your package, you can write and edit those parameter descriptions just in one place. However, keep in mind that you must point ``@inheritParams`` to the function where you originally define the parameters using ``@param``, not another function where you use the parameters but define them using an ``@inheritParams`` pointer.

If you want users to be able to directly use the function, you must include ``@export`` in your roxygen2 documentation. If you have written a function but then find it isn't being found when you try to compile a README file or vignette, a common culprit is that you have forgotten to export the function.

You can include formatting (lists, etc.) and equations in the roxygen2 documentation. Here are some of the common formatting tags you might want to use: `Table of common roxygen2 formatting tags <https://bookdown.org/rdpeng/RProgDA/documentation.html#common-roxygen2-formatting-tags>`_.

Some tips on using the R documentation format:

- Usually, you'll want you use the ``\link`` tag only in combination with the ``\code`` tag, since you're linking to another R function. Make sure you use these with ``\code`` wrapping ``\link``, not the other way around (``\code{\link{other_function}}``), or you'll get an error.
- Some of the equation formatting, including superscripts and subscripts, won't parse in Markdown-based documentation (but will for pdf-based documentation). With the ``\eqn`` and ``\deqn`` tags, you can include two versions of an equation, one with full formatting, which will be fully compiled by pdf-based documentation, and one with a reduced form that looks better in Markdown-based documentation (for example, ``\deqn{ \frac{X^2}{Y} }{ X2 / Y }``).
- For any examples in help files that take a while to run, you'll want to wrap the example code in the ``\dontrun`` tag.
- The tags ``\url`` and ``\href`` both include a web link. The difference between the two is that ``\url`` will print out the web address in the help documentation, ``\href`` allows you to use text other than the web address for the anchor text of the link. For example: ``"For more information, see \url{www.google.com}."``; ``"For more information, \href{www.google.com}{Google it}."``.

In addition to document functions, you should **also document any data** that comes with your package. To do that, create a file in the /R folder of the package called "``data.R``" to use to documentation all of the package's datasets. You can use ``roxygen2`` to document each dataset, and end each with the name of the dataset in quotation marks. There are more details on documenting package data using ``roxygen2`` in the next section.





Including data in a package
***************************

Many R packages are designed to manipulate, visualize, and model data so it may be a good idea for you to include some data in your package. The primary reason most developers include data in their package is to demonstrate how to use the functions included in the package with the included data. Creating a package as a means to distribute data is also a method that is gaining popularity. Additionally you may want to include data that your package uses internally, but is not available to somebody who is using your package. When including data in your package consider the fact that your **compressed package file should be smaller than 5MB**, which is the largest package size that CRAN allows. If your package is larger than 5MB make sure to inform users in the instructions for downloading and installing your package. 


