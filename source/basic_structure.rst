============================
Basic Structure of R package
============================

An R package begins life as a directory on your computer. This directory has a specific layout with specific files and sub-directories. The two required sub-directories are

- R, which contains all of your R code files
- man, which contains your documentation files.

At the top level of your package directory you will have a DESCRIPTION file and a NAMESPACE file. This represents the minimal requirements for an R package. Other files and sub-directories can be added and will discuss how and why in the sections below.

While RStudio is not required to build R packages, it contains a number of convenient features that make the development process easier and faster. That said, in order to use RStudio for package development, you must setup the environment properly. Details of how to do this can be found in Roger's `RStudio package development pre-flight check list <https://github.com/rdpeng/daprocedures/blob/master/lists/Rpackage_preflight.md>`_.




Building R Packages Pre-Flight Check List
*****************************************

1. Install latest version of R
2. Install latest version of RStudio
3. Open RStudio
4. Install ``devtools`` and ``usethis`` package (may take a few minutes) or update packages
5. Install ``roxygen2`` package
6. Click on Project ---> New Project ---> New Directory ---> R Package
7. Enter package name
8. Verify that project **subdirectory** name does not contain any spaces
9. Click "Create Project"
10. Delete bolierplate code and ``hello.R`` file in the ``R`` directory
11. Goto the ``man`` directory and delete the ``hello.Rd`` file
12. In File browser, click on the package name to go to the top level directory
13. Click "Build" tab in environment browser
14. Click More ---> "Configure Build Tools"
15. Check "Generate documentation with Roxygen" --> Click the "Configure..." button
16. Check "Build & Reload" in the Roxygen Options -> Click OK
17. Click OK in Project Build Tools Options






