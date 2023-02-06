.. _application:

****************
Getting familiar
****************

.. sidebar:: Summary

    :Info: Xperior basic concepts; things you should know when using the application on the daily basis...
    :Target: users
    :Status: mature

.. index:: single: concepts

After you successfully installed and ran the application, it is time to have a closer look on what is possible.
 
---------------------------

.. _appearance:

Appearence
----------

Xperior manages operations with child objects, special files; handles shortcuts events, toolbar events, ...

.. figure:: ../images/XPERIOR-block-structure.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Xperior Block Diagram 
    
Xperior application runs from network drive or locally. Automatically saves/loads user settings to/from Windows Registry system. 

.. _interpreter:

Build-in Python interpreter
---------------------------

Xperior application is completely based on `python programming language <http://www.python.org>`_. The python interpreter is contained in the form of :ref:`Shell <shell>` and :ref:`Editor <editor>`. You can use the Shell command window for executing the simple statements. 

.. _elogging:

Error Logging and Error Report 
------------------------------

Exceptional behavior caused by application itself, by error in expression in :ref:`Shell <shell>`, used script in :ref:`Communicator` or other source is logged and error can be reported. ``Error Report Form`` consist of *problem description* which should be filled by user and *log files* containing content of ``xperior_[PID].log`` file, versions of used modules and environment variables. By pressing the :guilabel:`&Generate to clipboard` all the text is generated into the clipboard and can be sent to a specified email address.

Following example shows a result of writing the :py:obj:`test` expression into the :ref:`Shell <shell>`. If test object is not defined, such Frame is shown. You can click to :guilabel:`&Send report` if You believe the bug should be fixed in the XPERIOR application itself. 

.. figure:: ../images/XPERIOR-Communicator-elog+ereport.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Error Logging and Error Report  

.. _logging:

Logging Facility 
----------------

Logging module (see Python's `logging module <http://docs.python.org/2.7/library/logging.html>`_) from default python distribution is used in Xperior application as well. Four loggers are introduced: *root, fapp, script, raw*.

* ``Root logger``: if any 3th party module is using logging module as well than output will be redirected to Xperior's :ref:`logging_trace` and the log file
* ``Fapp logger``: is internal logger informing the user about what the application is doing, for instance how long the script ran, which arguments are passed to VISA device instance, showing syntax error traceback, etc. The output of the logger is the :ref:`logging_trace` and the log file
* ``Script logger``: can be used in script itself, printing the output to the current stdout, which is normally :ref:`ptc_trace` or :ref:`shell`
* ``Raw logger``: is an internal logger

.. _logger_setup:

How to use a logger, change logging level 
*****************************************

When developing a script in :ref:`Communicator <communicator>`, you want to see intermediate logging outputs which may also be present in final version of your script. Using **print** statements is not an elegant solution and also requires to delete or comment out the statements after you finish debugging your code. With loggers you can just set the logging level in accordance to your current code stage. Use ``script logger`` like this::

 import logging 
 logger = logging.getLogger('script')
 logger.setLevel(logging.DEBUG) #logging.INFO after script development is finished
 #script code follows...
 logger.debug('this is a debug message')
 logger.info('this is an information')

You may also want to change the logging level of ``root logger`` or ``fapp logger`` in order to increase/decrease information verbosity::

 logging.getLogger().setLevel(logging.CRITICAL)
 logging.getLogger('fapp').setLevel(logging.CRITICAL)

.. warning:: When you start *xperior.exe --level=DEBUG* the logging level for both about mentioned loggers is set to DEBUG. DEBUG level is however recommended to application's development purposes only.

The relation between used loggers, handlers and formaters is shown in following figure. 

.. figure:: ../images/XPERIOR-logging_schematic.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Logging Facility 
    
.. _internal_access:

Accessing internal objects on runtime 
-------------------------------------

:ref:`Communicator's Commands Editor <editor>` and :ref:`shell` work with the same namespace. That means anything what is defined in Editor and passed to Interpreter (with Run button) is also accessible in Shell, and vice versa. In the same **globals** is stored special variable pointing to XPERIOR Application's internal objects. The variable's name is ``_int``.

The idea behind it is to offer XPERIOR and its sub-application's functionality to the User to fully automate her/his scripts. For example it is possible to use Extractor in scripts itself; make automatic entries of script results in :ref:`Reporter <reporter>`; initiate own Panel or Frames for user interaction; choosing visible sub-application in Notebook through code in :ref:`startup.py <startup>` file; etc.

Type ``_int.`` in :ref:`editor` or :ref:`shell` to activate AutoComplete Help which leads you further...


.. figure:: ../images/auto-complete_1.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Accessing Xperior's Main Frame object on runtime
    
Next Figure maps part of hierarchical distributions of internal objects. For complete map, source code needs to be analyzed by User her/himself. List below the Figure shows probably the most wanted objects to access. Short usage examples are included. 

.. figure:: ../images/XPERIOR-internal-objects.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Xperior Internal Objects

Following table shows some examples, it is not a complete list of all objects! ::

 # ------------------------------------------------------------------------------
 # Communicator:
 # ------------------------------------------------------------------------------
 _int.app.nb.communicator # Communicator Panel
 _int.editor # Editor's Notebook Manager
 _int.protocol # Protocol Trace Panel
 _int.app.vcp # Vertical Control Panel
 _int.app.nb.communicator.p # Path Panel
 # ------------------------------------------------------------------------------
 _int.editor.get_active_book() # Commands Editor STC
 _int.editor.efpath # Editor File Path - active book
 _int.app.nb.communicator.esp.editor.get_active_book().FoldAll() # 
 _int.shell # Interactive Console STC
 _int.shell.wrap(False) # wraping lines
 _int.shell.eframe.Show() # display Error Logging Frame (also when closed before)
 _int.interp # Python Interpreter
 _int.interp.compileAndRun(command) # 
 _int.interp.push(command) 
 _int.protocol # Protocol Trace STC
 _int.protocol.getTimeString() # current time like '17:15:38.688'
 _int.protocol.get_current_path() #get absolute path of generated protocol trace
 # ------------------------------------------------------------------------------
 # Reporter: 
 # ------------------------------------------------------------------------------
 _int.app.nb.reporter # Reporter Panel
 _int.app.nb.reporter.RunSelectedScript() #
 _int.app.nb.reporter.SaveReportsAndUpdate() #
 _int.app.nb.reporter.rp # Report Panel
 _int.app.nb.reporter.vcp # Vertical Control Panel
 # ------------------------------------------------------------------------------
 _int.app.nb.reporter.rp.rep # Report Class instance
 _int.app.nb.reporter.rp.GetScriptPath() #
 _int.app.nb.reporter.rp.ReloadAll() #
 
 _int.app.frame # main frame
 # dialog box example:
 def waitkey(message = None):
     """
     freeze script execution until user responds on initiated message box.
     """
     dlg = wx.MessageDialog(_int.app.frame, 1 and message or "press ok to continue", 
                            "Waitkey Message", style = wx.OK)
     try:
         dlg.ShowModal()
     except:
         pass
 
 _int.editor.efpath # path to opened file in Commands Editor
 # editor file path exapmle:
 if os.path.splitext(_int.editor.efpath)[1] != ".i3e":
     print "Not a python script for Xperior"
 
 _int.app.nb.reporter.rp.r.obj_data['TEST'] # name of selected script in Reporter
 # exapmle:
 if not _int.app.nb.reporter.rp.r.obj_data['TEST'] in _int.app.nb.communicator.esp.editor.efpath:
     waitkey("Please start this script from the Reporter (list selector needs to be active on that position).")
 
 _int.vcp.executeStop # Communicator's function
 # script stop exapmle:
 if something_goes_wrong_and_you_want_to_stop_the_script:
     _int.vcp.executeStop() # better: xlib.execute_stop() 
 
 _int.app.nb # Notebook
 # Notebook view exapmle, activate Extractor:
 _int.app.nb.SetSelection(2)
 
Most of the internal function calls or object accesses which are in general interest are exported into the :ref:`Xperior Library <xperior_lib>`. 
  