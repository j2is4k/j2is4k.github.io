.. _adv_concepts:

*****************
Advanced Concepts
*****************

.. sidebar:: Summary

    :Info: Xperior advanced concepts; things you would like to know in order to work more efficiently
    :Target: users
    :Status: mature

.. index:: single: advanced concepts

After you successfully installed and ran the application, it is time to have a closer look on what is available.

You can use direct navigation to the referenced documents:


.. toctree::
    :hidden:
    :maxdepth: 2
    :numbered:
    
    xlib
    multitesting
    remote_ctrl
    
---------------------------


.. _startup:

Startup File and Xperior Library
------------------------------

[:ref:`direct link <xperior_lib>`] 

Frequently used functions, variables, etc. can be defined and stored into the file. This process is implemented in two ways. So founded objects can be accessed with Communicator's :ref:`shell` or :ref:`editor`.

Object definitions from User point of view, such code changes or extensions are done in `Startup File`, file stored locally under user's application path. To access :ref:`Startup File <startup>` go to Edit -> Startup File.

:ref:`Xperior Library <xperior_lib>` is a form of objects definitions from administrator point of view. Anything defined this way will be accessible for every Xperior User. Code representing such definitions is content of :ref:`Xperior Library <xperior_lib>`. :ref:`Xperior Library <xperior_lib>` is handled as module on application start with syntax equivalent to ::
 
 import xlib

therefore all objects in xlib are accessed with ``xlib.[object_name]``. Startup File is equivalent to script run, therefore all object are available directly in application's namespace.


Multitesting
------------

[:ref:`direct link <multitest>`]

The way how to execute sequentionaly multiple test scenarios and report the corresponding verdicts. You can call it as **simple automation**. Please follow the :ref:`multitest` document for more information.


Remote Control
--------------

[:ref:`direct link <remote_ctrl>`]

Increasing number of test setups calls for administration and control possibility from a remote client host. An example is a *Admin* client controlling multiple servers, sending remote commands and fetching the remote objects for further evaluation. The typical usage is stopping/starting a script, getting the current status, executing remote processes, etc. How to configure the service, please refer to :ref:`remote_ctrl` .

