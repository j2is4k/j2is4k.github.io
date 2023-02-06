.. _xperior:

XPERIOR |version| documentation
=============================

Welcome! 

What is XPERIOR: test tool for the telecommunication branch written in Python programming language developed by `Noriba GmbH <http://www.noriba-it.com>`_ . Xperior aims on testing of devices connected to PC via `VISA <http://en.wikipedia.org/wiki/Virtual_Instrument_Software_Architecture>`_ interface, such **TCPIP**, **GPIB**, **USB**, **ASRL**, **TELNET**, etc. and supports `SOAP <http://en.wikipedia.org/wiki/SOAP>`_ communication. Application consists of built-in Python interpreter, giving the possibility to use huge amount of Python libraries in script itself. Maintenance of test results with Reporter offers clean overview and coordinates test planning.


Introduction
============

Xperior binds together more stand-alone applications and enables their information's exchange. Therefore also the name. If you are interested in certain sub-application, please refer direct to it.


Communicator
------------

:ref:`communicator` enables scripts execution, further data handling and direct interacting with built-in interpreter. Scripts can run in Python debugger. Useful functions defined in :ref:`Xperior Library <xperior_lib>`. Keyboard shortcut: :kbd:`Ctrl + F2`. 


Reporter
--------

:ref:`reporter` offers clear overview and multiple-users administration of bug reports with access to bug reporting server. Keyboard shortcut: :kbd:`Ctrl + F1`.


---------------------------

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version. 


---------------------------

Contents
========

.. toctree::
    :maxdepth: 2
    :numbered:
    
    rsts/install
    rsts/application
    rsts/communicator
    rsts/reporter
    rsts/adv_concepts
    rsts/examples
    

.. _documents_and_links:

Other Documents and Links
=========================

* General

 * `Noriba GmbH`_ - company profile
 * `software testing <http://en.wikipedia.org/wiki/Software_testing>`_ - provides an objective, independent view of the software to allow the business to appreciate and understand the risks at implementation of the software... 

* Python related

 * `Python Official Website <http://www.python.org/>`_ - Python is a dynamic object-oriented programming language that can be used for many kinds of software development. It offers strong support for integration with other languages and tools, comes with extensive standard libraries, and can be learned in a few days. Many Python programmers report substantial productivity gains and feel the language encourages the development of higher quality, more maintainable code.
 * `Python tutorial <http://docs.python.org/2/tutorial/>`_ - this python tutorial does not attempt to be comprehensive and cover every single feature, or even every commonly used feature. Instead, it introduces many of Python's most noteworthy features, and will give you a good idea of the language's flavor and style. After reading it, you will be able to read and write Python modules and programs, and you will be ready to learn more about the various Python library modules.
 * `Python for experienced <http://www.diveintopython.net/>`_ - is a Python book for experienced programmers.
 * `Python library reference <http://docs.python.org/2/library/>`_ - this library reference manual documents Python's standard library, as well as many optional library modules (which may or may not be available, depending on whether the underlying platform supports them and on the configuration choices made at compile time). It also documents the standard types of the language and its built-in functions and exceptions, many of which are not or incompletely documented in the Reference Manual.
 * `Reference manual <http://docs.python.org/2/reference/index.html>`_ - this reference manual describes the syntax and core semantics of the language. It is terse, but attempts to be exact and complete.
 * :pep:`0008` Style Guide for Python - this document gives coding conventions for the Python code comprising the standard library in the main Python distribution.




Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`


Contact
=======

For modules, documentation, unittest coverage and coding conventions is responsible the Noriba GmbH. Please contact us `support@noriba-it.com <http://noriba-it.com/contact>`_ for any further information or support.
