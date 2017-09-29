=================
testthat package
=================

The testthat package is designed to make it easy to setup a battery of tests for your R package. A nice introduction to the package can be found in Hadley Wickham's `article <https://journal.r-project.org/archive/2011-1/RJournal_2011-1_Wickham.pdf>`_ in the R Journal. Essentially, the package contains a suite of functions for testing function/expression output with the expected output. The simplest use of the package is for testing a simple expression:

.. code-block:: r
    :linenos:
    
    library(testthat)
    expect_that(sqrt(3) * sqrt(3), equals(3))
    
Note that the ``equals()`` function allows for some numerical fuzz, which is why this expression actually passes the test. When a test fails, ``expect_that()`` throws an error and does not return something.

.. code-block:: r
    :linenos:
    
    ## Use a strict test of equality (this test fails)
    expect_that(sqrt(3) * sqrt(3), is_identical_to(3))

    Error: sqrt(3) * sqrt(3) not identical to 3.
    Objects equal but not identical
    
    
The ``expect_that()`` function can be used to wrap many different kinds of test, beyond just numerical output. Following list provides a brief summary of the types of comparisons that can be made.


equals()
  check for equality with numerical fuzz
is_identical_to()
  strict equality via identical()
is_equivalent_to()
  like ``equals()`` but ignores object attributes
is_a()
  checks the class of an object (using ``inherits()``)
matches()
  checks that a string matches a regular expression
prints_text()
  checks that an expression prints to the console
shows_message()
  checks for a message being generated
gives_warning()
  checks that an expression gives a warning
throws_error()
  checks that an expression (properly) throws an error
is_true()
  checks that an expression is TRUE
  
A collection of calls to ``expect_that()`` can be put together with the ``test_that()`` function, as in

.. code-block:: r
    :linenos:
    
    test_that("model fitting", {
        data(airquality)
        fit <- lm(Ozone ~ Wind, data = airquality)
        expect_that(fit, is_a("lm"))
        expect_that(1 + 1, equals(2))
    })



Typically, you would put your tests in an R file. If you have multiple sets of tests that test different domains of a package, you might put those **tests in different files**. Individual files can have their tests run with the ``test_file()`` function. A collection of tests files can be placed in a directory and tested all together with the ``test_dir()`` function.

In the context of an R package, it makes sense to put the test files in the ``tests/`` directory. This way, when running R CMD check (see the next section) all of the tests will be run as part of process of checking the entire package. If any of your tests fail, then the entire package checking process will fail and will prevent you from distributing buggy code. If you want users to be able to easily see the tests from an installed package, you can place the tests in the ``inst/tests`` directory and have a separate file in the tests directory run all of the tests.
