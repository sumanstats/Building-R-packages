==================
Knitr and Markdown
==================




Both vignette and README files can be written as R Markdown files, which will allow you to include R code examples and results from your package. One of the most exciting tools in R is the knitr system for combining code and text to create a reproducible document. In terms of the power you get for time invested in learning a tool, knitr probably can't be beat. Everything you need to know to create and "knit" a reproducible document can be learned in about 20 minutes, and while there is a lot more you can do to customize this process if you want to, probably 80% of what you'll ever want to do with knitr you'll learn in those first 20 minutes.

R Markdown files are mostly written using Markdown. To write R Markdown files, you need to understand what markup languages like Markdown are and how they work. In Word and other word processing programs you have used, you can add formatting using buttons and keyboard shortcuts (e.g., "Ctrl-B" for bold). The file saves the words you type. It also saves the formatting, but you see the final output, rather than the formatting markup, when you edit the file (WYSIWYG - what you see is what you get). In markup languages, on the other hand, you markup the document directly to show what formatting the final version should have (e.g., you type \**bold\** in the file to end up with a document with bold). Examples of markup languages include:

- HTML (HyperText Markup Language)
- LaTex
- Markdown (a "lightweight" markup language)

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
    


