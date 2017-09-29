==============================
Software Design and Philosophy
==============================

Introduction
************

Writing and designing software is a creative endeavour and like in other creative arts there are styles are guidelines that you can follow, however revolutions in the field can occur when those dogmas are broken properly. We're going to cover a few of the prominent ideas in software design in the last century. Above all of these suggestions I suggest one cardinal rule: Have empathy for your fellow human beings. Software is inherently complex, so set up your users to `fall into a pit of success <https://blogs.msdn.microsoft.com/brada/2003/10/02/the-pit-of-success/>`_.

The Unix Philosophy
*******************

The R programming language is open source software and many open source software packages draw some inspiration from the design of the Unix operating system which macOS and Linux are based on. Ken Thompson - one of the designers of Unix - first laid out this philosophy, and many Unix philosophy principles can be applied to R programs. The overarching philosophical theme of Unix programs is to do one thing well. Sticking to this rule accomplishes several objectives:

1. Since your program only does one thing the chance that your program contains many lines of code is reduced. This means that other's can more easily read the code for your program so they can understand exactly how it works (if they need to know).
2. Simplicity in your program reduces the chance there will be major bugs in your program since fewer lines of code means fewer opportunities to make a mistake.
3. Your program will be easier for users to understand since the number of inputs and outputs are reduced for a program that only does one thing.
4. Programs built with other small programs have a higher chance of also being small. This ability to string several small programs together to make a more complex (but also small) program is called composability.

Unix command line programs are notable for their use of the pipe operator (|) and so the Unix philosophy also encourages programs to produce outputs that can be piped into program inputs. Recently pipes in R have surged in popularity thanks to projects like the ``magrittr`` package. When it makes sense for your function to take data (usually a vector or a data frame) as an argument and then return data, you should consider making the data argument the first argument in your function so that your function can be part of a **data pipeline**.

One case where many ``R`` programs differ from the greater Unix philosophy is in terms of user interaction. Unix programs will usually only print a message to the user if a program produces an error or warning. Although this is a good guideline for your programs, many R programs print messages to the console even if the program works correctly. Many R users only use the language interactively, so showing messages to your users might make sense for your package. One issue with messages is that they produce output which is separate from the results of your program, and therefore messages are harder to capture.

Default Values
**************

Every function argument is an opportunity for your function to fail the user by producing an error because of bad or unexpected inputs. Therefore you should provide as many default values for your functions as is reasonable. If there's an argument in your function that should only be one of a handful of values you should use the match.arg() function to check that one of the permitted values is provided:

.. code-block:: r
    :linenos:

    multiply_by <- function(n, multiplier = c("two", "three", "four")){
    multiplier <- match.arg(multiplier)
    if(multiplier == "two"){
      n * 2
    } else if(multiplier == "three"){
      n * 3
    } else {
      n * 4
    }
    }

    multiply_by(5, "two")
    [1] 10
    multiply_by(5, "six")
    Error in match.arg(multiplier): 'arg' should be one of "two", "three", "four"



Using ``match.arg()`` ensures that an error is thrown immediately if an erroneous argument value is provided.

Naming things
*************

Naming functions and variables is a challenge that programmers have always struggled with. Here are a few strategies you should use when naming things in R:

- Use snake case and lowercase. Modern R packages use function and variable names like ``geom_line()``, ``bind_rows()``, and ``unnest_token()`` where words are separated by underscores (_) and all characters are lowercase. Once upon a time words were commonly separated by periods (.) but that scheme can cause confusion with regard to generic functions (see the object oriented programming chapter for more information).

- Names should be short. A short name is faster to type and is more memorable than a long and complicated name. The length of a variable name has to be balanced with the fact that:

- Names should be meaningful and descriptive. Function names should generally describe the actions they perform. Other object names should describe the data or attributes they encompass. In general you should avoid numbering variable names like apple1, apple2, and apple3. Instead you should create a data structure called apples so you can access each apple with apple[[1]], apple[[2]], and apple[[3]].

- Be sure that you're not assigning names that already exist and are common in R. For example mean, summary, and rt are already names of functions in R, so try to avoid overwriting them. You can check if a name is taken using the ``apropos()`` function:

.. code-block:: r
    :linenos:

    apropos("mean")
     [1] ".colMeans"     ".rowMeans"     "colMeans"      "kmeans"
     [5] "mean"          "mean.Date"     "mean.default"  "mean.difftime"
     [9] "mean.POSIXct"  "mean.POSIXlt"  "rowMeans"      "weighted.mean"
    apropos("my_new_function")
    character(0)
    
You might want to consider grouping similar functions together in families which all start with the same short prefix. For example in the ggplot2 package the ``aes_`` family of functions set graphing aesthetics, the ``gs_`` family of functions interact with the Google Sheets API in the googlesheets package, and the ``wq_`` family of functions all write questions in the swirlify package.

Playing well with others
************************

If you write a package with useful functions that are well designed then you may be lucky enough that your package becomes popular! Others may build upon your functions to extend or adapt thier features for other purposes. This means that when you establish a set of arguments for a function you're implicitly promising some amount of stability for the inputs and outputs of that function. Changing the order or the nature of function arguments or return values can break other people's code, creating work and causing pain for those who have chosen to use your software. For this reason you should think very carefully about function arguments and outputs to ensure that both can grow and change sustainably. You should seek to strike a balance between frustrating your users by making breaking changes and ensuring that your package follows up to date programming patterns and ideas. If you believe that the functions in a package you're developing are not yet stable you should make users aware of that fact so that they're warned if they choose to build on your work.

Summary
*******

Most of software design is ensuring that your users stumble into their desired outcome. You may think you're writing the most intuitive package, but sitting down with a colleague and watching them use your package can teach you volumes about what users want and expect out of your package. There are libraries full of books written about software design and this chapter is only meant to serve as a jumping off point. If you happen to be looking for inspiration we highly recommend this talk Bret Victor called: `The Future of Programming <http://worrydream.com/dbx/>`_.

