===========================
NAMESPACE function notation
===========================



As you start to use many packages in R, the likelihood of two functions having the same name increases. For example, the commonly used dplyr package has a function named filter(), which is also the name of a function in the stats package. If one has both packages loaded (a more than likely scenario) how can one specific exactly which filter() function they want to call?

In R, every function has a full name, which includes the package namespace as part of the name. This format is along the lines of

.. code-block:: r
    :linenos:
    
    <package name>::<exported function name>
    
For example, the filter() function from the dplyr package can be referenced as dplyr::filter(). This way, there is no confusion over which filter() function we are calling. While in principle every function can be referenced in this way, it can be tiresome for interactive work. However, for programming, it is often safer to reference a function using the full name if there is even a chance that there might be confusion.

It is possible to call functions **that are not exported by package** by using the namespace notation. The ::: operator can be used for this purpose, as in <package name>:::<unexported function name>. This can be useful for examining the code of an unexported function (e.g. for debugging purposes) or for temporarily accessing some unexported feature of a package. However, it's not a good idea to make this a habit as such unexported functions may change or even be eliminated in future versions of the package. Furthermore, use of the ::: operator is not allowed for packages that reside on CRAN.





