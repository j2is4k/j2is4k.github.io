.. _xperior_lib:

*************
Xperior Library 
*************

.. sidebar:: Summary

    :Info: concept of additional configurations, features and services. It is recommended to use existing code to avoid `reinventing the wheel <http://en.wikipedia.org/wiki/Reinventing_the_wheel>`_. Other modules similar to xlib can and are presented in xlib as well, extending such code and structuring it into groups. 
    :Target: users
    :Status: mature

.. index:: single: advanced concepts

Functions, procedures, classes, etc. - generally objects coded in xlib.py file, comes with version of XPERIOR. Users are encouraged to use xlib's objects in test scripts itself to simplify and improve the coding. The backward compatibility of objects defined in xlib is mather of discipline of file developers

---------------------------

Figure shows which kind of libraries is used by the application.

.. figure:: ../images/XPERIOR-libraries.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Xperior Libraries 

Usage
=====

All of the "objects" described are accessible from xlib object in current namespace. The reason is clarity. 

.. figure:: ../images/XPERIOR-xlib-global_1.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Accessing functions 

.. figure:: ../images/XPERIOR-xlib-global_2.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Getting tips 

API description
===============

Classes
-------

.. autoclass:: xlib.Cleartool
   :members:
   :undoc-members:
   
.. autoclass:: xlib.MessageDialog
   :members:
   :undoc-members:
   
Functions
---------

.. automodule:: xlib
   :members: