=====================
Open Source Licensing
=====================


Overview
********

You can specify how your R package is licensed in the package DESCRIPTION file under the License: section. How you license your R package is important because it provides a set of constraints for how other R developers use your code. If you're writing an R package to be used internally in your company then your company may choose to not share the package. In this case licensing your R package is less important since the package belongs to your company. In your package DESCRIPTION you can specify License: file LICENSE, and then create a text file called LICENSE which explains that your company reserves all rights to the package.

However if you (or your company) would like to publicly share your R package you should consider open source licensing. The philosophy of open source revolves around three principles:

- The source code of the software can be inspected.
- The source code of the software can be modified.
- Modified versions of the software can be redistributed.

Nearly all open source licenses provide the protections above. Let's discuss three of the most popular open source licenses among R packages.


The General Public License
**************************

Known as the GPL, the GNU GPL, and GPL-3, the General Public License was originally written by Richard Stallman. The GPL is known as a copyleft license, meaning that any software that is bundled with or originates from software licensed under the GPL must also be released under the GPL. The exacting meaning of "bundle" will depend a bit on the circumstances. For example, software distributed with an operating system can be licensed under different licenses even if the operating system itself is licensed under the GPL. You can use the GPL-3 as the license for your R package by specifying **License: GPL-3** in the DESCRIPTION file.

It is worth noting that R itself is licensed under version 2 of the GPL, or GPL-2, which is an earlier version of this license.


The MIT License
***************

The MIT license is a more permissive license compared to the GPL. MIT licensed software can be modified or incorporated into software that is not open source. The MIT license protects the copyright holder from legal liability that might be incurred from using the software. When using the MIT license in a R package you should specify **License: MIT + file LICENSE** in the DESCRIPTION file. You should then add a file called ``LICENSE`` to your package which uses the following template exactly:


.. code-block:: none
    :linenos:
    
    YEAR: [The current year]
    COPYRIGHT HOLDER: [Your name or your organization's name]
    
The CC0 License
***************

The `Creative Commons <https://creativecommons.org/>`_ licenses are usually used for artistic and creative works, however the CC0 license is also appropriate for software. The CC0 license dedicates your R package to the public domain, which means that you give up all copyright claims to your R package. The CC0 license allows your software to join other great works like Pride and Prejudice, The Adventures of Huckleberry Finn, and The Scarlet Letter in the public domain. You can use the CC0 license for your R package by specifying **License: CC0** in the DESCRIPTION file.


