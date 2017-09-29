============
Testing Code
============


Once you've written code for an R package and have gotten that code to a point where you believe it's working, it may be a good time to step back and consider a few things about your code.

- How do you know it's working? Given that you wrote the functions, you have a certain set of expectations about how the functions should behave. Specifically, for a given set of inputs you expect a certain output. Having these expectations clearly in mind is an important aspect of knowing whether code is "working".
- Have you already tested your code? Chances are, throughout the development of your code, you ran little tests to see if your functions were working. Assuming these tests were valid for the code you were testing, it's worth keeping these tests on hand and making them part of your package.


Setting up a battery of tests for the code in your package can play a big role in maintaining the ongoing smooth operation of the package in hunting down bugs in the code, should they arise. Over time, many aspects of a package can change. Specifically:

- As you actively develop your code, you may change/break older code without knowing it. For example, modifying a helper function that lots of other functions rely may be better for some functions but may break behavior for other functions. Without a comprehensive testing framework, you might not know that some behavior is broken until a user reports it to you.
- The environment in which your package runs can change. The version of R can change, libraries, web sites and any other external resources, and packages can all change without warning. In such cases, your code may be unchanged, but because of an external change, your code may not produce the expected output given a set of inputs. Having tests in place that are run regularly can help to catch these changes even if your package isn't under active development.
- As you fix bugs in your code, it's often a good idea to include a specific test that addresses each bug so that you can be sure that the bug does not "return" in a future version of the package (this is also known as a regression).


Testing your code effectively has some implications for code design. In particular, it may be more useful to divide your code into smaller functions that you can test individual pieces more effectively. For example, if you have one large function that returns TRUE or FALSE, it is easy to test this function, but ultimately it may not be possible to identify problems deep in the code by simply checking if the function returns the correct logical value. It may be better to divide up large function into smaller functions so that core elements of the function can be tested separately to ensure that they are behaving appropriately.
