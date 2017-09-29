==================
Knitr and Markdown
==================




Both vignette and README files can be written as R Markdown files, which will allow you to include R code examples and results from your package. One of the most exciting tools in R is the ``knitr`` system for combining code and text to create a reproducible document. In terms of the power you get for time invested in learning a tool, ``knitr`` probably can't be beat. Everything you need to know to create and "knit" a reproducible document can be learned in about 20 minutes, and while there is a lot more you can do to customize this process if you want to, probably 80% of what you'll ever want to do with knitr you'll learn in those first 20 minutes.

R Markdown files are mostly written using Markdown. To write R Markdown files, you need to understand what markup languages like Markdown are and how they work. In Word and other word processing programs you have used, you can add formatting using buttons and keyboard shortcuts (e.g., "Ctrl-B" for bold). The file saves the words you type. It also saves the formatting, but you see the final output, rather than the formatting markup, when you edit the file (WYSIWYG - what you see is what you get). In markup languages, on the other hand, you markup the document directly to show what formatting the final version should have (e.g., you type \**bold\** in the file to end up with a document with bold). Examples of markup languages include:

- HTML (HyperText Markup Language)
- LaTex
- Markdown (a "lightweight" markup language)
- restructuredText

To write a file in Markdown, you'll need to learn the conventions for creating formatting. See this table for some common formatting choices: `Table of Markdown Formatting Specifiers <https://bookdown.org/rdpeng/RProgDA/documentation.html#common-markdown-formatting-elements>`_.

Some other simple things you can do in Markdown include:

- Lists (ordered or bulleted)

- Equations

- Tables

- Figures from file

- Block quotes

- Superscripts

The start of a Markdown file gives some metadata for the file (authors, title, format) in a language called YAML. For example, the YAML section of a package vignette might look like this:


.. code-block:: r
    :linenos:
    
    ---
    title: "Model Details for example_package"
    author: "Jane Doe"
    date: "2016-11-08"
    output: rmarkdown::html_vignette
    vignette: >
      %\VignetteIndexEntry{Model Details for example_package}
      %\VignetteEngine{knitr::rmarkdown}
      %\VignetteEncoding{UTF-8}
    ---
    

When creating R Markdown documents using the RStudio toolbar, much of this YAML will be automatically generated based on your specifications when opening the initial file. However, this is not the case with package vignettes, for which you'll need to go into the YAML and add the authors and title yourself. Leave the vignette engine, vignette encoding, output, and date as their default values.

For more Markdown conventions, see RStudio's R Markdown Reference Guide (link also available through "Help" in RStudio).

R Markdown files work a lot like Markdown files, but add the ability to include R code that will be run before rendering the final document. This **functionality is based on literate programming, an idea developed by Donald Knuth,** to mix executable code with regular text. The files you create can then be rendered, to run any embedded code. The final output will have results from your code and the regular text.

1. The basic steps of opening and rendering an R Markdown file in RStudio are:
2. To open a new R Markdown file, go to "File" -> "New File" -> "RMarkdown" -> for now, choose a "Document" in "HTML" format.
3. This will open a new R Markdown file in RStudio. The file extension for R Markdown files is ".Rmd".
4. The new file comes with some example code and text. You can run the file as-is to try out the example. You will ultimately delete this example code and text and replace it with your own.
5. Once you "knit" the R Markdown file, R will render an HTML file with the output. This is automatically saved in the same directory where you saved your .Rmd file.
6. Write everything besides R code using Markdown syntax.


The ``knit`` function from the `knitr <https://cran.r-project.org/web/packages/knitr/index.html>`_ package works by taking a document in R Markdown format (among a few possible formats), reading through it for any markers of the start of R code, running any of the code between that "start" marker and a marker showing a return to regular Markdown, writing any of the relevant results from R code into the Markdown file in Markdown format, and then passing the entire document, now in Markdown rather than R Markdown format, to software that can render from Markdown to the desired output format (for example, compile a pdf, Word, or HTML document).

This means that all a user needs to do to include R code, that will be run if desired, within a document is to properly separate it from other parts of the document through the appropriate markers. To indicate R code in an RMarkdown document, you need to separate off the code chunk using the following syntax:

.. code-block:: r
    :linenos:
  
    ```{r}
    my_vec <- 1:10
    ```

This syntax tells R how to find the start and end of pieces of R code when the file is rendered. R will walk through, find each piece of R code, run it and create output (printed output or figures, for example), and then pass the file along to another program to complete rendering (e.g., Tex for pdf files).

You can specify **a name for each chunk**, if you'd like, by including it after "``r``" when you begin your chunk. For example, to give the **name load_mtcars to a code chunk** that loads the mtcars dataset, specify that name in the start of the code chunk:

.. code-block:: r
    :linenos:
    
    ```{r load_mtcars}
    data(mtcars)
    ```
    
Here are a couple of tips for **naming code chunks**:

- Chunk names must be unique across a document.
- Any chunks you don't name are given ordered numbers by ``knitr``.

You do not have to name each chunk. However, there are some advantages:

- It will be easier to find any errors.
- You can use the chunk labels in referencing for figure labels.
- You can reference chunks later by name.








