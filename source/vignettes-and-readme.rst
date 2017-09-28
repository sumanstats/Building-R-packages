==========================
Vignettes and Readme files
==========================


You will likely want to create a document that walks users through the basics of how to use your package. You can do this through two formats:

- **Vignette**: This document is bundled with your R package, so it becomes locally available to a user once they install your package from CRAN. They will also have it available if they install the package from GitHub, as long as they use the build_vignettes = TRUE when running install_github.
- **README file**: If you have your package on GitHub, this document will show up on the main page of the repository.

A package likely only needs a README file if you are posting the package to GitHub. For any GitHub repository, if there is a README.md file in the top directory of the repository, it will be rendered on the main GitHub repository page below the listed repository content. For an example, visit https://github.com/leighseverson/countyweather and scroll down. You'll see a list of all the files and subdirectories included in the package repository and below that is the content in the package's README.md file, which gives a tutorial on using the package.

If the README file does not need to include R code, you can write it directly as an .md file, using Markdown syntax, which is explained in more detail in the next section. If you want to include R code, you should start with a README.Rmd file, which you can then render to Markdown using knitr. You can use the ``devtools`` package to add either a README.md or README.Rmd file to a package directory, using ``use_readme_md`` or ``use_readme_rmd``, respectively. These functions will add the appropriate file to the top level of the package directory and will also add the file name to ".Rbuildignore", since having one of these files in the top level of the package directory could otherwise cause some problems when building the package.

The README file is a useful way to give GitHub users information about your package, but it will not be included in builds of the package or be available through CRAN for packages that are posted there. Instead, if you want to create tutorials or overview documents that are included in a package build, you should do that by adding one or more package vignettes. Vignettes are stored in a ``vignettes`` subdirectory within the package directory.

To add a vignette file, saved within this subdirectory (which will be created if you do not already have it), use the ``use_vignette`` function from devtools. This function takes as arguments the file name of the vignette you'd like to create and the package for which you'd like to create it (the default is the package in the current working directory). For example, if you are currently working in your package's top-level directory and you would like to add a vignette called "model_details", you can do that with the code:

.. code-block:: r
    :linenos:
    use_vignette("model_details")
    
You can have more than one vignette per package, which can be useful if you want to include one vignette that gives a more general overview of the package as well as a few vignettes that go into greater detail about particular aspects or applications.

Once you create a vignette with ``use_vignette``, be sure to update the Vignette Index Entry in the ``vignette's YAML`` (the code at the top of an R Markdown document). Replace "Vignette Title" there with the actual title you use for the vignette.





