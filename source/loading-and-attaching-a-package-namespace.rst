==========================
NAMESPACE: load and attach
==========================


Loading and attaching namespace
*******************************


When dealing with R packages, it's useful to understand the distinction between loading a package namespace and attaching it. When package A imports the namespace of package B, package A loads the namespace of package B in order to gain access to the exported functions of package B. However, when the namespace of package B is loaded, it is only available to package A; it is not placed on the search list and is not visible to the user or to other packages.

Attaching a package namespace places that namespace on the search list, making it visible to the user and to other packages. Sometimes this is needed because certain functions need to be made visible to the user and not just to a given package.



