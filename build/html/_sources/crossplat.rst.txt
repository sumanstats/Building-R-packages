===========================
Cross Platform Development
===========================


Overview
********

One of the great features about R is that you can run R code on multiple kinds of computers and operating systems and it will behave the same way on each one. Most of time you don't need to worry about what platform your R code is running on. The following sections discuss strategies and functions that you should use to ensure that your R code runs uniformly on every kind of system.

Handling paths
**************

Paths to files and folders can have big differences between operating systems. In general you should avoid constructing a path "by hand." For example if I wanted to access a file called ``data.txt`` that I know will be located on the user's desktop using the string ``"~/Desktop/data.txt"`` would not work if that code was run on a Windows machine. In general you should always use functions to construct and find paths to files and folders. The correct programmatic way to construct the path above is to use the ``file.path()`` function. So to get the file above I would do the following:

.. code-block:: r
    :linenos:

    file.path("~", "Desktop", "data.txt")
    [1] "~/Desktop/data.txt"

Note that this book is probably being built on a Mac:

.. code-block:: r
    :linenos:

    Sys.info()['sysname']
      sysname
    "Darwin"

If the resulting line above says "Darwin" it's refering to the core of macOS. If you don't have a Mac try running both lines of code above to see the resulting path and the type of system that you're running.

In general it's not guaranteed on any system that a particular file or folder you've looking for will exist - however if the user of your package has installed your package you can be sure that any files within your package exist on their machine. You can find the path to files included in your package using the ``system.file()`` function. Any files or folders in the ``inst/`` directory of your package will be copied one level up once your package is installed. If your package is called ggplyr2 and there's file in your package under inst/data/first.txt you can get the path to that file with system.file("data", "first.txt", package = "ggplyr2"). Packaging files with your package is the best way to ensure that users have access to them when they're using your package.

In terms of constructing paths there are a few other functions you should be aware of.
Remeber that the results for many of these functions are contingent on this book being built on a Mac, so if you're using Windows I encourage you to run these functions yourself to see their result. The ``path.expand()`` function is usually used to find the absolute path name of a user's home directory when the tilde (~) is inlcuded in the path. The tilde is a shortcut for the path to the current user's home directory. Let's take a look at ``path.expand()`` in action:


.. code-block:: r
    :linenos:

    path.expand("~")
    [1] "/Users/ashish"
    path.expand(file.path("~", "Desktop"))
    [1] "/Users/ashish/Desktop"

The ``normalizePath()`` function is built on top of ``path.expand()``, so it includes path.expand()'s features but it also creates full paths for other shortcuts like "." which signifies the current working directory and ".." which signifies the directory above the current working directory. Let's take a look at some examples:

.. code-block:: r
    :linenos:

    normalizePath(file.path("~", "R"))
    [1] "/Users/ashish/R"
    normalizePath(".")
    [1] "/Users/ashish/books/msdr"
    normalizePath("..")
    [1] "/Users/ashish/books"

To extract parts of a path you can use the basename() function to get the name of the file or the deepest directory in the path and you can use dirname() to get the part of the path that does not include either the file or the deepest directory. Let's take a look at some examples:


.. code-block:: r
    :linenos:

    data_file <- normalizePath(file.path("~", "data.txt"))
    data_file
    [1] "/Users/ashish/data.txt"
    dirname(data_file)
    [1] "/Users/ashish"
    dirname(dirname(data_file))
    [1] "/Users"
    basename(data_file)
    [1] "data.txt"


Saving Files & rappdirs
***********************

CRAN's policy for R packages contains the following statement:

.. code-block:: none
    :linenos:

    Packages should not write in the users' home filespace, nor anywhere else on the file system apart from the R session's
    temporary directory (or during installation in the location pointed to by TMPDIR: and such usage should be cleaned up).
    Installing into the system's R installation (e.g., scripts to its bin directory) is not allowed.
    Limited exceptions may be allowed in interactive sessions if the package obtains confirmation from the user.


In general you should strive to get the user's consent before you create or save files on their computer. With some functions consent is implicit, for example it's clear somebody using ``write.csv()`` consents to producing a csv file at a specified path. When it's not absolutely clear that the user will be creating a file or folder when they use your functions you should ask them specifically. Take a look at the code below for a skeleton of a function that asks for a user's consent:


.. code-block:: r
    :linenos:

    #' A function for doing something
    #'
    #' This function takes some action. It also attempts to create a file on your
    #' desktop called \code{data.txt}. If \code{data.txt} cannot be created a
    #' warning is raised.
    #'
    #' @param force If set to \code{TRUE}, \code{data.txt} will be created on the
    #' user's Desktop if their Desktop exists. If this function is used in an
    #' interactive session the user will be asked whether or not \code{data.txt}
    #' should be created. The default value is \code{FALSE}.
    #'
    #' @export
    some_function <- function(force = FALSE){

      #
      # ... some code that does something useful ...
      #

      if(!dir.exists(file.path("~", "Desktop"))){
        warning("No Desktop found.")
      } else {
        if(!force && interactive()){
          result <- select.list(c("Yes", "No"),
                      title = "May this program create data.txt on your desktop?")
          if(result == "Yes"){
            file.create(file.path("~", "Desktop", "data.txt"))
          }
        } else if(force){
          file.create(file.path("~", "Desktop", "data.txt"))
        } else {
          warning("data.txt was not created on the Desktop.")
        }
      }
    }



The ``some_function()`` function above is a contrived example of how to ask for permission from the user to create a file on their hard drive. Notice that the description of the function clearly states that the function attempts to create the data.txt file. This function has a force argument which will create the data.txt file without asking the user first. By setting force = FALSE as the default, the user must set force = TRUE, which is one method to get consent from the user. The function above uses the ``interactive()`` function in order to determine whether the user is using this function in an R console or if this function is being run in a non-interactive session. If the user is in an interactive R session then using select.list() is a decent method to ask the user a question. You should strive to use ``select.list()`` and ``interactive()`` together in order to prevent an R session from waiting for input from a user that doesn't exist.

rappdirs
********

Even the contrived example above implicitly raises a good question: where should your package save files? The most obvious answer is to allow the user to provide an argument for the path where a file should be saved. This is a good idea as long as your package won't need to depend on the location of that file in the future, for example if your package is creating an output data file. But what if you need persistent and consistent access to a file? You might be tempted to use ``path.package()`` in order to find the directory that your package is installed in so you can store files there. This isn't a good idea because file access permissions often do not allow users to modify files where R packages are stored.

In order to find a location where you can read and write files that will persist on a user's computer you should use the rappdirs package. This package contains functions that will return paths to directories where you package can store files for future use. The ``user_data_dir()`` function will provide a user-specific path for your package, while the ``site_data_dir()`` function will return a directory path that is shared by all users. Let's take a look at rappdirs in action:

.. code-block:: r
    :linenos:

    library(rappdirs)
    Loading required package: methods
    site_data_dir(appname = "ggplyr2")
    [1] "/Library/Application Support/ggplyr2"
    user_data_dir(appname = "ggplyr2")
    [1] "/Users/ashish/Library/Application Support/ggplyr2"
    
Both of the examples above are probably the Mac-specific paths. We can get the Windows specific paths by specifying the os argument:

.. code-block:: r
    :linenos:

    user_data_dir(appname = "ggplyr2", os = "win")
    [1] "C:/Users/<username>/Local/ggplyr2/ggplyr2"
    
If you don't supply the os argument then the function will determine the operating system automatically. One feature about ``user_data_dir()`` you should note is the roaming = TRUE argument. Many Windows networks are configured so that any authorized user can log in to any computer on the network and have access to their desktop, settings, and files. Setting roaming = TRUE returns a special path so that R will have access to your packages files everywhere, but this requires the directory to be synced often. Make sure to only use roaming = TRUE if the files your package will storing with rappdirs are going to be small. For more information about rappdirs see https://github.com/hadley/rappdirs.


Options and Starting R
**********************

Several R Packages allow users to set global options that effect the behavior of the package using the options() function. The options() function returns a list, and named values in this list can be set using the following syntax: options(key = value). It's a common feature for packages to allow a user to set options which may specify package defaults, or change the behavior of the package in some way. You should thoroughly document how your package is effected by which options are set.

When an R session begins a series of files are searched for and run if found as detailed in help("Startup"). One of those files is .Rprofile. The .Rprofile file is just a regular R file which is usually located in a user's home directory (which you can find with normalizePath("~")). A user's .Rprofile is run every time they start an R session, so it's a good file for setting options that a user wants to be set when using R. If you want a user to be able to set an option that is related to your package that is unlikely to change (like a username or a key), then you should consider instructing them to create or make changes to their .Rprofile.

Package Installation
********************

Your package documentation should prominently feature installation instructions. Many R packages that are distributed through GitHub recommend installing the devtools package, and then using ``devtools::install_github()`` to install the package. The devtools package is wonderful for developing R packages, but it has many dependencies whhich can make it difficult for users to install. I recommend instructing folks to use the ghit package by Thomas Leeper and the ghit::install_github() function as a reliable alternative to devtools.

In cases where users might have a weak internet connection it's often easier for a user to download the source of your package as a zip file and then to install it using ``install.packages()``. Instead of asking users to discern the path of zip file they've downloaded you should ask them to enter ``install.packages(file.choose(), repos = NULL, type = "source")`` into the R console and then they can interactively select the file they just downloaded. If a user is denied permission to modify their local package directory, they still may be able to use a package if they specify a directory they have access to with the lib argument for ``install.packages()``.


Environmental Attributes
************************



Personally you may need to know specific information about the hardware and software limitations of the computer that is running your R code. The environmental variables ``.Platform`` and ``.Machine`` are lists which contain named elements that can tell your program about the underlying machine. For example ``.Platform$OS.type`` is a good method for checking whether your program is in a Windows environment since the only values it can return are "windows" and "unix":


.. code-block:: r
    :linenos:
    
    .Platform$OS.type
    [1] "unix"
    
    
For more information about information contained in ``.Platform`` see the help file: ``help(".Platform")``.

The ``.Machine`` variable contains information specific to the computer architecture that your program is being run on. For example ``.Machine$double.xmax`` and ``.Machine$double.xmin`` are respectively the largest and smallest positive numbers that can be represented in R on your platform:


.. code-block:: r
    :linenos:
    
    .Machine$double.xmax
    [1] 1.797693e+308
    .Machine$double.xmax + 100 == .Machine$double.xmax
    [1] TRUE
    .Machine$double.xmin
    [1] 2.225074e-308
    
You might also find ``.Machine$double.eps`` useful, which is the smallest number on a machine such that ``1 + .Machine$double.eps != 1`` evaluates to TRUE:

.. code-block:: r
    :linenos:
    
    1 + .Machine$double.eps != 1
    [1] TRUE
    1 + .Machine$double.xmin != 1
    [1] FALSE 
    

Summary
*******


File and folder paths differ across platforms so R provides several functions to ensure that your program can construct paths correctly. The ``rappdirs`` package helps further by identifying locations where you can safely store files that your package can access. However before creating files anywhere on a user's disk you should always ask the user's permission. You should provide clear and easy instructions so people can easily install your package. The ``.Platform`` and ``.Machine`` variables can inform your program about hardware and software details.

    
    