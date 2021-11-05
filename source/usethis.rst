===============
usethis package
===============

``usethis`` is a workflow package: it automates repetitive tasks that arise during project setup and development, both for R packages and non-package projects.

-----
Usage
-----

Most ``use_*()`` functions operate on the *active project*: literally, a
directory on your computer. If you’ve just used usethis to create a new
package or project, that will be the active project. Otherwise, usethis
verifies that current working directory is or is below a valid project
directory and that becomes the active project. Use ``proj_get()`` or
``proj_sitrep()`` to manually query the project and `read more in the
docs <http://usethis.r-lib.org/reference/proj_get.html>`_.

A few usethis functions have no strong connections to projects and will
expect you to provide a path.

usethis is quite chatty, explaining what it’s doing and assigning you
tasks. ``✔`` indicates something usethis has done for you. ``●`` indicates
that you’ll need to do some work yourself.




.. note::
   Before using ``usethis`` functions, make sure to get a PAT from GitHub and store it in GITHUB_PAT envrironment variable. 
   If it is already available, no need to set this. The easiest way to get PAT is with ``usethis`` and then store it in git credentials. 
   
   
   .. code-block:: r
        
       usethis::create_github_token()
       gitcreds::gitcreds_set()
       
   The other way is to use ``credentials::set_github_pat()``. If you want to drop existing GITHUB_PAT and ask for a new one, run 
   ``credentials::set_github_pat(force_new = TRUE)``.



Below is a quick look at how usethis can help to set up a package. But
remember, many usethis functions are also applicable to analytical
projects that are not packages.

.. code-block:: r

    library(usethis)

    # Create a new package -------------------------------------------------
    tmp <- file.path(tempdir(), "mypkg")
    create_package(tmp)
    #> ✔ Setting active project to '/private/var/folders/vr/gzrbtprx6ybg85y5pvwm1ct40000gn/T/RtmpGwzXO5/mypkg'
    #> ✔ Creating 'R/'
    #> ✔ Creating 'man/'
    #> ✔ Writing 'DESCRIPTION'
    #> ✔ Writing 'NAMESPACE'

    # Modify the description ----------------------------------------------
    use_mit_license("My Name")
    #> ✔ Setting License field in DESCRIPTION to 'MIT + file LICENSE'
    #> ✔ Writing 'LICENSE.md'
    #> ✔ Adding '^LICENSE\\.md$' to '.Rbuildignore'
    #> ✔ Writing 'LICENSE'

    use_package("MASS", "Suggests")
    #> ✔ Adding 'MASS' to Suggests field in DESCRIPTION
    #> ● Use `requireNamespace("MASS", quietly = TRUE)` to test if package     is installed
    #> ● Then use `MASS::fun()` to refer to functions.

    use_dev_package("callr")
    #> ✔ Adding 'callr' to Imports field in DESCRIPTION
    #> ✔ Adding 'r-lib/callr' to Remotes field in DESCRIPTION

    # Set up various packages ---------------------------------------------
    use_roxygen_md()
    #> ✔ Setting Roxygen field in DESCRIPTION to 'list(markdown = TRUE)'
    #> ✔ Setting RoxygenNote field in DESCRIPTION to '6.1.0'
    #> ● Run `devtools::document()`

    use_rcpp()
    #> ✔ Adding 'Rcpp' to LinkingTo field in DESCRIPTION
    #> ✔ Adding 'Rcpp' to Imports field in DESCRIPTION
    #> ✔ Creating 'src/'
    #> ✔ Adding '*.o', '*.so', '*.dll' to 'src/.gitignore'
    #> ● Include the following roxygen tags somewhere in your package
    #>   #' @useDynLib mypkg, .registration = TRUE
    #>   #' @importFrom Rcpp sourceCpp
    #>   NULL
    #> ● Run `devtools::document()`

    use_revdep()
    #> ✔ Creating 'revdep/'
    #> ✔ Adding '^revdep$' to '.Rbuildignore'
    #> ✔ Adding 'checks', 'library', 'checks.noindex', 'library.noindex', 'data.sqlite', '*.html' to 'revdep/.gitignore'
    #> ✔ Writing 'revdep/email.yml'
    #> ● Run checks with `revdepcheck::revdep_check(num_workers = 4)`

    # Set up other files -------------------------------------------------
    use_readme_md()
    #> ✔ Writing 'README.md'

    use_news_md()
    #> ✔ Writing 'NEWS.md'

    use_test("my-test")
    #> ✔ Adding 'testthat' to Suggests field in DESCRIPTION
    #> ✔ Creating 'tests/testthat/'
    #> ✔ Writing 'tests/testthat.R'
    #> ✔ Writing 'tests/testthat/test-my-test.R'

    x <- 1
    y <- 2
    use_data(x, y)
    #> ✔ Creating 'data/'
    #> ✔ Saving 'x', 'y' to 'data/x.rda', 'data/y.rda'

    # Use git ------------------------------------------------------------
    use_git()
    #> ✔ Initialising Git repo
    #> ✔ Adding '.Rhistory', '.RData', '.Rproj.user' to '.gitignore'






Other useful functions are 


.. list-table:: Other useful **usethis** functions
   :widths: 25 55
   :header-rows: 1

   * - Functions
     - Use

   * - **use_description**
     - Create or modify ``DESCRIPTION``     
   * - **edit_r_profile**
     - opens ``.Rprofile``
   * - **edit_r_environ**
     - opens ``.Renviron``
   * - **edit_r_makevars**
     - opens ``.R/Makevars``
   * - **use_r**
     - Create or edit ``R`` script files
   * - **use_package**
     - Adds a CRAN package dependency to DESCRIPTION
   * - **use_import_from**
     - Imports a function from another package by adding the roxygen2 ``@importFrom`` tag to the package-level documentation. Importing a function from another package allows you to refer to it without a namespace (e.g., ``fun()`` instead of ``package::fun()``).
   * - **use_c**
     - Adds infrastructure needed to use compiled code
   * - **use_cpp11**
     - Use C++ via the ``cpp11`` package
   * - **use_vignette**
     - Create a vignette
   * - **use_travis**
     - Enable CI using Travis, creates ``.travis.yml`` with basic configuration for testing
   * - **use_github_actions**
     - Sets up continuous integration (CI) using GitHub Actions
   * - **use_appveyor**
     - Enable CI using AppVeyor, creates ``appveyor.yml`` with basic configuration for testing 
   * - **use_circleci**  
     - Enable CI using CircleCI, creates ``.circleci/config.yml`` with basic configuration for testing 
   * - **use_coverage**
     - Adds test coverage reporting to a package
   * - **use_logo**
     - Adds a logo to a package     
   * - **use_cran_comments**
     - Create a file where you can add comments to include with your CRAN submission
   * - **use_readme_rmd** 
     - Set up the package to include a README file in Rmarkdown format. So rich intermingling of code and output is possible.
   * - **use_news_md**
     - Add a file to the package to give news on changes in new versions 


