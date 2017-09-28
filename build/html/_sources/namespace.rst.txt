==============
NAMESPACE file
==============

The NAMESPACE file specifies the interface to the package that is presented to the user. This is done via a series of export() statements, which indicate which functions in the package are exported to the user. Functions that are not exported cannot be called directly by the user (although see below). In addition to exports, the NAMESPACE file also specifies what functions or packages are imported by the package. If your package depends on functions from another package, you must import them via the NAMESPACE file.

Below is the NAMESPACE file for the mvtsplot package described above.

.. code-block:: r
    :linenos:
    
    export("mvtsplot")

    import(splines)
    import(RColorBrewer)
    importFrom("grDevices", "colorRampPalette", "gray")
    importFrom("graphics", "abline", "axis", "box", "image",     "layout",
           "lines", "par", "plot", "points", "segments",   "strwidth",
           "text", "Axis")
    importFrom("stats", "complete.cases", "lm", "na.exclude", "predict",
           "quantile")
           

Here we can see that only a single function is exported from the package (the mvtsplot() function). There are two types of import statements:

- **import()**, simply takes a package name as an argument, and the interpretation is that all exported functions from that external package will be accessible to your package

- **importFrom()**, takes a package and a series of function names as arguments. This directive allows you to specify exactly which function you need from an external package. For example, this package imports the colorRampPalette() and gray() functions from the grDevices package.

Generally speaking, it is better to use importFrom() and to be specific about which function you need from an external package. However, in some cases when you truly need almost every function in a package, it may be more efficient to simply import() the entire package.

With respect to exporting functions, it is important to think through carefully which functions you want to export. First and foremost, exported functions must be documented and supported. Users will generally expect exported functions to be there in subsequent iterations of the package. It's usually best to limit the number of functions that you export (if possible). It's always possible to export something later if it is needed, but removing an exported function once people have gotten used to having it available can result in upset users. Finally, exporting a long list of functions has the effect of cluttering a user's namespace with function names that may conflict with functions from other packages. Minimizing the number of exports reduces the chances of a conflict with other packages (using more package-specific function names is another way).



