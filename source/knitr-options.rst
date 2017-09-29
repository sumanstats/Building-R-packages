====================
Common Knitr options
====================

You can also add options when you start a chunk. Many of these options can be set as TRUE / FALSE and include: `Table of Common knitr Options <https://bookdown.org/rdpeng/RProgDA/documentation.html#common-knitr-chunk-options>`_.

To include any of these options, add the option and value in the opening brackets and separate multiple options with commas:

.. code-block:: r
    :linenos:
    
    ```{r  messages = FALSE, echo = FALSE}
    mtcars[1, 1:3]
    ```
    
You can set "global" options at the beginning of the document. This will **create new defaults for all of the chunks** in the document. For example, if you want ``echo, warning, and message`` to be FALSE by default in all code chunks, you can run:


.. code-block:: r
    :linenos:
    
    ```{r  global_options}
    knitr::opts_chunk$set(echo = FALSE, message = FALSE,
    warning = FALSE)
    ```
   
If you set both global and local chunk options for a chunk, **local** chunk options **will take precedence** over global options. For example, running a document with:

.. code-block:: r
    :linenos:
    
    ```{r  global_options}
    knitr::opts_chunk$set(echo = FALSE, message = FALSE,
    warning = FALSE)
    ```


    ```{r  check_mtcars, echo = TRUE}
    head(mtcars, 1)
    ```

would print the code for the ``check_mtcars`` chunk, because the option specified for that specific chunk (echo = TRUE) would override the global option (echo = FALSE).

You can also include R output directly in your text ("inline") using backticks:

"There are \`r nrow(mtcars)\` observations in the mtcars data set. The average miles per gallon is \`r mean(mtcars$mpg, na.rm = TRUE)\`."

Once the file is rendered, this gives:

"There are 32 observations in the mtcars data set. The average miles per gallon is 20.090625."

Here are some tips that will help you diagnose some problems rendering R Markdown files:

- Be sure to save your R Markdown file before you run it.
- All the code in the file will run "from scratch"- as if you just opened a new R session.
- The code will run using, as a working directory, the directory where you saved the R Markdown file.

You'll want to try out pieces of your code as you write an R Markdown document. There are a few ways you can do that:

- You can run code in chunks just like you can run code from a script (Ctrl-Return or the "Run" button).
- You can run all the code in a chunk (or all the code in all chunks) using the different options under the "Run" button in RStudio.
- All the "Run" options have keyboard shortcuts, so you can use those.

You can use this format to create documentation, including vignettes, to give users advice and examples for using your package.

Two excellent books for learning more about creating reproducible documents with R are Dynamic Documents with R and knitr by Yihui Xie (the creator of knitr) and Reproducible Research with R and RStudio by Christopher Gandrud. The first goes into the technical details of how knitr and related code works, which gives you the tools to extensively customize a document. The second provides an extensive view of how to use tools from R and other open source software to conduct, write up, and present research in a reproducible and efficient way. RStudio's `R Markdown Cheatsheet <https://www.rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf>`_ is another very useful reference.




