.. _multitest:

************
Multitesting
************

.. sidebar:: Summary

    :Info: The way how to execute sequentionaly multiple test scenarios and report the corresponding verdicts. You can call it as **simple automation**.
    :Target: users
    :Status: mature

.. index:: single: multitesting

In the multitest procedure an extra script is created. This script executes multiple scripts and for particular test result creates a report entry in Reporter. Some parts in original script have special meaning, please see Other recommendations for further information.

---------------------------

.. figure:: ../images/XPERIOR-Multiscript.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Multitest Idea


General description
===================

Control units
-------------

* ``Use Reporter`` - checkbox, defines if automated reporting should be used at all.
* ``Major Version`` - choice control, represents group of reports with common factor (e.g. software release or final version). Every single reports file on your drive mirrors one of the major version. By default is selected the same one you have in :ref:`Reporter`.
* ``Minor Version`` - text control, is string value of certain version of software under test (e.g. beta version or daily build).
* ``Search path`` - text control, specifies start directory of "top-down file search" including wildcard. Files searched here are your scripts (testscripts).
* ``Logs path`` - text control, in special cases, the scripts generate additional logs. Where should these be stored?
* ``File mask`` - text control, scripts wildcard.
* ``Found scripts`` - list control, is list of all available scripts, excluding all 'multitest' scripts. Listed files can by marked 4 different ways. 
    

.. figure:: ../images/XPERIOR-Multitesting-dialogbox.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Multiscript selector
    

Associated symbols
------------------

* ``Brick icon with add symbol`` - indicates that script is located also in Reporter -> everything is configured properly for multitesting 
* ``Brick icon with exclamation symbol`` - the multitest session will be started, but with no automated test result entries to Reporter due disabled Use Reporter checkbox
* ``Brick icon with delete symbol`` - means that you still want to use automated test result entries to Reporter, but filename cannot be found there. Particular test will not be started unless you uncheck Use Reporter or reconfigure Reporter
* ``Exclamation icon with delete symbol`` - indicates that test name is restricted and not recommended to use

How to use
==========

Learning by example, use existing multitesting example at **[Xperior distribution]\addons\multitesting**:

* select Reporter -> Select Reports -> [Xperior distribution]\addons\multitesting\reports -> select any version
* select Reporter -> Select Scripts -> [Xperior distribution]\addons\multitesting
* select Communicator -> Open [Xperior distribution]\addons\multitesting\MultiTest.i3e -> Run
* Run generated multitest 


Note: in Multitest Dialogbox if you want to change Search path, do it. Press Rescan for update. If you are also using Reporter for your test result administration, you should see brick icon with add symbol in Found scripts field. To correct your Reporter settings use Reporter -> Select Reports and Reporter -> Select Scripts. Uncheck Use Reporter to disable automated result entries. The raw results will be still available in ``*.ptc`` (protocol) file.


Rules
=====

1. There shouldn't be any user interaction inside a script. Exceptions are waitkeys which are automatically disabled if multitesting is active. Use instead of **wx.Dialog** derivates the **xlib.Dialog** forms. Dialog will be than always answered with wx.OK if multitesting is active.
2. Script names have to use characters usable for (python) function definition.
3. SCRIPT_DIR is a special variable name holding an absolute path to original script directory in multitest session and will be overwritten only if it's declaration is present in original script. Lets consider following::

    #original script at D:\work\test_set_1\validation.i3e
    SCRIPT_DIR = xlib.get_script_dir()
    TEST_MODULE_PATH = SCRIPT_DIR + r'\test_module'

    #multitest script collecting more "original scripts" generated at D:\work\multitest.i3e
    SCRIPT_DIR = "D:\work\test_set_1" #parser replacement!
    TEST_MODULE_PATH = SCRIPT_DIR + r'\test_module'

    ##You are than adressing the same test module path.

4. Certain conventions needs to be fulfilled in order to achieve correct Reporter entries. stdout will be redirected for further (Reporter) processing between ## conclusion and ##-. See Script template.
5. Use proper header part of the script, see Script template.


Other recommendations
=====================

1. Used scripts are time-finite ones. These can be functional scripts or stability-stress tests.
2. Use limited quantity of information in Errors class instance.
3. Better more short scripts as few longer. 