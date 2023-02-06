.. _install:

***************
Getting started
***************

.. sidebar:: Summary

    :Info: You will find here information how to download, install and start the Xperior application with various command line options.
    :Target: users
    :Status: mature



---------------------------

.. index:: single: download

How to download
===============

Please contact us via `email <http://www.noriba-it.com/contact-us/>`_.


.. index:: single: installation

How to install
==============

XPERIOR Application runs Python interpreter and requires certain site-packages to operate properly. In best case, you get XPERIOR Application as msi installer with the complete python distribution. If so, just proceed the installation steps and run the application from your desktop.

You may also receive msi installer without python distribution, than you need to fulfill certain preconditions.

Prerequisites
-------------

Prerequisite Table

======================  ============  ======
Application or package  Version       Note
======================  ============  ======
**Python**              **2.7.5**     **mandatory**
**wxPython**            **2.8.12.1**  **mandatory**
xmlplus                 0.8.4         optional for SOAP
ZSI                     2.0           optional for SOAP
SUDS                    0.4           optional for SOAP - 2nd generation client
Pyro4                   4.22          optional for application remote control
matplotlib              1.3.1         optional for 2D & 3D graphs support, a.o.
numpy                   1.8.0         optional for 2D & 3D graphs support, a.o.
scipy                   0.13.0        optional
py2exe                  0.6.9         optional
pywin32                 218           optional
NI-488.2                > 2.4         optional for remote device communication
NI-VISA                 > 3.6         optional for remote device communication
======================  ============  ======


Application Version
-------------------

Version of XPERIOR is in this format: **A.B.CD**

* **A**: major python interpreter change. 1. for Python 2.x series, 2. for Python 3.x series
* **B**: major XPERIOR feature change
* **C**: minor XPERIOR feature change/important bugfix of B
* **D**: beta version, non critical bugfixes of C 

  E.g.: 1.8.0a is Python 2.x interpreter version with major feature change since 1.7.0. It is the first and beta version since the 1.7.0. Higher risk of bugs can be expected. 


How to run
==========

.. index:: single: command line options

Command-line options
--------------------

Xperior executable located at [Xperior distribution]\xperior.exe supports following startup options

.. option:: -h , -l <LEVEL>, -e <bool exit on stop>, -r <bool no reporter>, -f <no_xlib>, script_path

   Run a module as a script.

.. figure:: ../images/XPERIOR-startup_help.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Startup Shell info  
    
.. figure:: ../images/XPERIOR-startup_shell_info.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Startup Shell info  
   
   
   
Also as shown in figure above, ``_int.app.frame.comm.abort_exit_on_stop`` function has been added. Exit on stop is not proceeded if unhandled exception in script occours.