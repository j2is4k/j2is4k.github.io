.. _communicator:

************
Communicator
************

.. sidebar:: Summary

    :Info: Communicator, a control part encapsulating the code editor, interactive shell and related addons.
    :Target: users
    :Status: mature

.. index:: single: communicator

Communicator is the combination of :ref:`GUI Editor <editor>`, *special libraries* (graphs ploting, text frames, SOAP network procedures, instruments communication (ASRL, GPIB, TCPIP, TELNET, USB, etc.)) and **built-in Python interpreter** offering wide spectrum of very useful modules. 

Also enables changes of :ref:`internal attributes <internal_access>` of Xperior application. Defining own functions or modules and importing them on start or store them as :ref:`macros`, makes the application to suit to almost anybody. Developing phase can be improved by using the :ref:`debugger`. Console mode called :ref:`com_light` compiled to an executable file can be used for special non-GUI embedded cases.


---------------------------

.. _com_general:

General description
-------------------

Functionality and GUI items description.


.. _editor:

Editor
******

Is a notebook containing pages, where a page represents a source code (file) which is a runnable script in Python interpreter. This source code shares the same namespace with `shell`_ console. Don't miss useful tips in the chapter :ref:`script_temp`. 

Shortcut to Commands editor is :kbd:`Alt + F1`.


.. _shell:

Shell
*****

Command line Interactive Python console (Shell) shares the same namespace with `editor`_. To learn more about Python syntaxes, programming strategies and descriptions of huge number of modules, see :ref:`documents_and_links`.

Shortcut to Shell is :kbd:`Alt + F2`.

.. warning:: Command entered to the `shell`_ is executed in the main thread, therefore long term operation, infinitive loops, deep recursions, etc. lead to application freeze.

*Based on Patrick K. O'Brien's "shell.py" module.* *VISA implementation is based on Torsten Bronger's "visa.py" and "vpp43.py" module.*




Namespace Tree
**************

Displays namespace structure in expandable tree form. Entry point is ``locals()``, a dictionary listing all namespace objects by its name. Further on every such object can contain further (nested) objects in a tree form. Right panel contains additional information about selected item:

* complete namespace path
* type of object
* value of object
* docstring
* source code 

Double left clicking on tree item will print the complete namespace path in `shell`_.

*Based on Patrick K. O'Brien's "filling.py" module.*

.. figure:: ../images/XPERIOR-Communicator-namespace_tree.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Example of Namespace Tree

    
Explorer
********

File-system Explorer. It allows to open files in `editor`_ comfortably (with ``LeftDClick`` or via ``RightClick Menu``) or start the file with system call.

.. figure:: ../images/XPERIOR-Communicator-explorer.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Explorer


.. _ptc_trace:

Protocol Trace
**************

Captures the standard output of the script and is a target for the :ref:`script logger <logger_setup>` and :ref:`VISA <visa_config>` and :ref:`SOAP <soap_config>` communication. Protocol trace is a standard text field, with additional methods for buffering input strings and for limiting maximal number of displayed lines.

Script logger logs in format (see how to setup the :ref:`script logger <logger_setup>`)::

    hh:mm:ss.mis [LEVEL   ] (  thread:module~function:line) message

VISA and SOAP communication is logged in format::

    hh:mm:ss.mis        device_name:             request
    hh:mm:ss.mis        device_name:  dddd.d ms  response


.. figure:: ../images/XPERIOR-Communicator-protocol_trace.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Example of Procotol Trace output


.. _logging_trace:

Logging Trace
*************

Displaying logger informing the user about what the application is doing, for instance how long the script ran, which arguments are passed to VISA device instance, showing syntax error traceback, etc. Is a target for :ref:`root <logger_setup>` and :ref:`fapp logger <logger_setup>`

Logger logs in format:

    hh:mm:ss.mis [LEVEL    ] (        logger-thread:module:line) message

    
.. figure:: ../images/XPERIOR-Communicator-logging_trace.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Example of Logging Trace output


Vertical Control Panel
**********************

Description of control units

==================  ===============  ===========
Name                Widget Type      Description
==================  ===============  ===========
*Run*               Button           :kbd:`Ctrl + R` - starts a new thread with parsing content of Commands Editor as a source to python's interpreter.
*Debug Run*         Button           :kbd:`Ctrl + D` - prepares the script as debuggee server to wait for external debugger. Details here.
*Pause*             Button           :kbd:`Ctrl + P` - pauses/unpauses a script started by Run button.
*Force Stop*        Button           :kbd:`Ctrl + T` - terminates running script. 
*Logging Type*      Radio Button     defines which kind of logging should be used. Recommended is "both".
*Max Screen Lines*  Text Control     parameter defines maximal displayed number of lines in Protocol Trace. 
*Window Split*      Radio Button     specifies the sash orientation between EditorAndShell Panel and Protocols Panel. 
*Instrument*        Choice Control   lists all active instruments. Click on <new> for on-fly instrument declaration. You may want to use this object in connection with Macros.
*Reload Devices*    Button reloads   (reinstatiate) already defined VISA and SOAP objects, see VISA and SOAP configuration. 
*Macro Setup*       Button controls  configurable buttons. Separately discussed in :ref:`macros`. 
==================  ===============  ===========


.. _visa_config:

Instrument Configuration
------------------------

Before addressing any instrument, it needs to be added to the **Instruments Configuration**. After starting the Xperior Application choose :menuselection:`Edit -> Instrument Configuration`. This will bring up the Instruments Configuration screen illustrated in figure below. To apply changes for VISA devices, you don't need to restart XPERIOR, just save the modified file and press ``Reload Devices`` button.

.. figure:: ../images/instrument_ini_example1.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Instrument Configuration
    
List of devices displays all configurations and the connection status. Three states are defined: 
    
    1) enabled and active 
    2) enabled and inactive
    3) disabled
    
In the column *Enabled*, you will find green checkmarks or red crosses. By clicking on this column, you can change a checkmark to a cross and vice versa and thus enabling or disabling the use of this instrument.

.. note:: Every time the List of devices is reloaded, the Xperior Application will try to establish a connection to all enabled instruments and then lists if the connection is active in the column *Connection*. You can speed up this process by disabling all the instruments known to be switched off or not connected. An instrument will be accessible in scripts only if it is enabled and its *Connection* column marks it as active. To update the connection status, press ``Save & Reload`` button. 

You can *Insert* and *Remove Instrument* definitions with appropriate buttons or keyboard keys.

**Parameters Editor** enables configuration for selected device. Every *Interface Type* contains different set of parameters. Notice the difference e.g. for ``TCPIP_VXI_11`` and ``TCPIP_SOCKET``. On the left side are mandatory parameters, on the right optional *VI Attributes*. Specified VI Attribute (not <default>) has precedence.

Add and Remove Instruments
**************************

On the **Instruments Configuration** screen you will see a list of *Instruments*. By clicking on any of the list entries, you can edit the instruments configuration like VISA connection type, host name or timeout. By clicking on the button ``Insert`` or pressing the ``Insert`` key, you add a new, empty list entry. This new entry will automatically be selected, so you can start editing it.

The following Settings can be made:

==========================  ===========
Option                      Description
==========================  ===========
Interface Type              type of physical connection like LAN, GPIB or USB
Device Name                 name that will be used in scripts to identify the instrument; the termination chars can be left blank for the default setting
Timeout                     time in seconds that the Xperior Application waits for a response from an instrument before showing a timeout error
Delay                       time in milliseconds after each write command to the instrument
Settings on the left side   specific for the selected Interface Type and configured connection; they will be addressed separately in the following subchapters
Settings on the right side  VISA attributes that should only be configured by advanced users; for more information on these attributes please consult the VISA documentation 
==========================  ===========

Alternatively, you can add an instrument for just one session by using the Instrument Dropdown menu in the Vertical Control Panel on the left. Just open the :menuselection:`Dropdown menu->choose <new>`. This will open up the **Instrument Connection Configuration** window. Instruments added through this dialog will not be saved. After closing and restarting the Xperior Application, those instruments will no longer be available.

.. figure:: ../images/XPERIOR-Communicator-macro-setup+vcp.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Vertical Control Panel
    

.. figure:: ../images/instrument_ini_example2.png
    :align: left
    :figwidth: 100 %
    
    Figure: Instrument Connection Configuration
    
In the **Instrument Connection Configuration** window (<new>), the following attributes can be changed:

==============================  ===========
Option                          Description
==============================  ===========
Alias                           equals the Device Name on the Instruments Configuration screen
Device Type                     equals the Interface Type
The Number                      used in the case of multiple adapters on the PC and can be 0 in most cases
Timeout and Delay               correspond to the attributes of the same name on the Instruments Configuration screen
The Identifier(IP or Hostname)  is specific for the selected Device Type and will become a part of the VISA RSC field
==============================  ===========

Advanced users who are familiar with VISA address strings can directly edit the ``VISA RSC field``.


Interface ASRL (VISA)
*********************

To control an Instrument via the serial port, choose Interface Type ASRL. There you have to configure the resource name (COM1, COM2 etc), the baud rate, number of data bits, number of stop bits and the parity check method to use. You cannot configure a serial connection in the **Instrument Connection Configuration** window.

Interface GPIB (VISA)
*********************

To configure General Purpose Interface Bus (GPIB) connection choose :menuselection:`Interface->Device Type GPIB`.

* **Instruments Configuration** screen: here you have to configure the primary address of the instrument. A secondary address can also be specified, if certain device requires it.
* **Instrument Connection Configuration** window: enter the primary GPIB address as Identifier. If you wish to configure a secondary address, add it to the Identifier after the primary address separated by two colons ``::``.


Interface RSNRP (VISA)
**********************

To control RSNRP from a PC, you need to install the NRP Toolkit which is supplied with any NRP device. You also need the NRP-NI-VISA Passport. After connecting the NRP device to your PC, run VISA interactive control (from the :menuselection:`StartMenu->Programs->National Instruments->VISA->VISA Interactive Control`). It will list all currently connected instruments. There, you'll find a VISA address string in the syntax::

    RSNRP::<model code>::<serial number>::INSTR

* **Instruments Configuration** screen: insert model code and serial number into the respective fields.
* **Instrument Connection Configuration** window: for the connection to work, the VISA RSC field must contain the same string as is displayed in VISA Interactive Control. So you need to write ``<model code>::<serial number>`` as Identifier. The *Identity* field will be ignored. Finally, you will have to edit the field VISA RSC manually to remove the 0 of RSNRP0.


Interface TCPIP_SOCKET (VISA)
*****************************

Generally, you should use the *VXI LAN interface* to configure a connection via LAN. But in some cases you might want to configure the connection more specifically. For those situations, you can use socket communication, also known as *Raw Ethernet* communication. Choose :menuselection:`Interface->Device Type->TCPIP_SOCKET`.

* **Instruments Configuration** screen: like with the TCPIP_VXI_11 Interface Type, the host name can be the network device name or the IP address of the instrument. The port number is the number of the network port on the instrument that you are connecting to.
* **Instrument Connection Configuration** window: time same rules applies.

.. note:: This configuration lacks some important trigger and hand shaking functions. It is recommended to use the VXI LAN interface instead.


Interface TCPIP_VXI_11 (VISA)
*****************************

To address an instrument connected by LAN you should usually choose :menuselection:`Interface->Device Type->TCPIP_VXI_11`. Here, you have to configure the following attributes:

* **Instruments Configuration** screen: the host name can be the instrument network device name or the IP address. The Identity is not mandatory unless there is more than one VISA entity running on the same instrument. In that case, inst0 would be the first VISA entity, inst1 the second etc.
* **Instrument Connection Configuration** window: the Identifier equals the host name and can be network device name or IP address. The Identity, like above, is not mandatory unless there is more than one VISA entity running on the same instrument. In that case, inst0 would be the first VISA entity, inst1 the second etc.


Interface TELNET
****************

Unlike the other interfaces, telnet does not use the VISA interface but establishes a simple TCP connection. It's configuration uses the same parameters as TCPIP socket, but the VISA attributes will not be available. You cannot configure a telnet connection in the **Instrument Connection Configuration** window.

.. note:: This configuration lacks some important trigger and hand shaking functions. It is recommended to use the VXI LAN interface instead.


Interface USB (VISA)
********************

To connect an instrument via USB, you need to know the *vendor id*(VID), *product id*(PID) and *serial number*. If you have NI VISA installed, it will automatically detect the instrument once it has been connected to the computer via USB. To get the required parameters, run VISA interactive control (:menuselection:`StartMenu->Programs->National Instruments->VISA->VISA Interactive Control`). It will list all currently connected instruments. There, you'll find a VISA address string in the syntax:

    USB0::<vendor id>::<productid>::<serial number>::INSTR

* **Instruments Configuration** screen: enter the vendor id(VID), product id(PID) and serial number into the respective fields.
* **Instrument Connection Configuration** window: for the connection to work, the VISA RSC field must contain the same string as is displayed in VISA Interactive Control. So you need to write <vendor id>::<productid>::<serial number> as Identifier. The Identity field will be ignored.


Export and Import instrument configuration
******************************************

Selecting other device from *List of devices* saves the changes for current device virtually. All changes are first stored into the file with ``Save & Reload`` button. ``Close`` will discard all virtual changes. ``Import`` and ``Export`` buttons realise corresponding functionality.


.. _soap_config:

SOAP Devices Configuration
--------------------------

To enter the configuration panel, go to :menuselection:`Edit->SOAP Configuration`, illustration in figure below. Panel elements general description is the same as in previous paragraph. To apply changes for SOAP devices, you don't need to restart XPERIOR, just save the modified file, press ``Reload Devices`` button.

.. figure:: ../images/soap_py_example1.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: SOAP Devices Configuration


Protocol Trace Configuration
----------------------------

Communicator's relevant settings such last opened file, logging type, sash position, editor zoom, etc. are stored in windows registry. Values are overwritten/updated when closing the XPERIOR.

Switching On/Off Device logging
*******************************

Introducing protocol logging control for SOAP and Instrument devices: Implicitly protocol logging is enabled. You can turn it off these ways:

.. code-block:: python

    _int.use_protocol(False) #to disable logging for every instance
    [device].use_protocol(False) #to disable logging only for specified device

First option has higher priority. The protocol logging can be activated again by passing True argument or by restarting the XPERIOR. In `shell`_ the logging is always active.


Absolute vs Relative timestamps logging
***************************************

Timestamps related with logging of VISA & SOAP devices can now be displayed in relative mode - timestamps displaying elapsed time since script start, or absolute mode - displaying current PC clock time. Use respective function calls:

.. code-block:: python

    _int.vcp.use_absolute_stamp() 
    _int.vcp.use_relative_stamp()


.. _script_temp:

Writing down a script
---------------------

If you've never programmed in python, read the tutorial first (see :ref:`documents_and_links`). Next step is to examine the VISA devices communication. Make sure, you've configured everything correctly and start with simple commands such: ``[device_allias].ask('*opt?')``. You can than extend the `shell`_ commands to a simple script, storing the result of *ask() method* to some variable and manipulating this variable. The best way of learning is to read the code written by your colleagues. Don't forget that your code will be also read!

.. note:: It is important that we synchronize with using certain style when writing the script in Python. To increase readability and clarity please use Style Guide for Python.


Script template
***************

If you want to use other XPERIOR feature, such as :ref:`multitest` or :ref:`reporter`, you should use following script template. Using template of header part ensures proper parsing of contained information. The same is valid for conslusion part.

Script template can be downloaded :download:`../../../addons/template_generator.i3e`. Just start the script in the `editor`_.

.. figure:: ../images/XPERIOR-Communicator-ScriptTemplate.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Script template


Xperior library (xlib)
--------------------

XPERIOR library is concept of additional configurations, features and services. Separately discussed in page :ref:`xperior_lib`.


Plot a graph
************

Part of :ref:`xperior_lib` is also a plot library. Plot of graphs is easy and even more if you are familiar with MATLAB. For detailed information refer to `matplotlib <http://matplotlib.org/>`_. You can use plot function defined in :ref:`xlib <xperior_lib>`, shell: ``xlib.plot()``. Here are some graph examples with source files locations:

* Location: :download:`../../../source/examples/matplotlib_graph/3d_sphere.i3e`
* Location: :download:`../../../source/examples/matplotlib_graph/3d_f&t_allocation.i3e`
* Location: :download:`../../../source/examples/matplotlib_graph/coh+csd.i3e`
* Location: :download:`../../../source/examples/matplotlib_graph/noise.i3e`
* Location: :download:`../../../source/examples/matplotlib_graph/errbar.i3e`
* Location: :download:`../../../source/examples/matplotlib_graph/histogram.i3e`
    

.. image:: ../images/XPERIOR-Communicator-3d_sphere.jpg
    :width: 30 %
    :alt: Example 3D 1 - Sphere


.. image:: ../images/XPERIOR-Communicator-3d_f&t_allocation.jpg
    :width: 30 %
    :alt: Example 3D 2 - Frequency-time allocation

    
.. image:: ../images/XPERIOR-Communicator-plot-cod+csd.jpg
    :width: 30 %
    :alt: Example 4 - Coherence & cross spectral density of two signals

    
.. image:: ../images/XPERIOR-Communicator-plot-noise.jpg
    :width: 30 %
    :alt: Example 1 - Gaussian noise

    
.. image:: ../images/XPERIOR-Communicator-plot-errbar.jpg
    :width: 30 %
    :alt:  Example 2 - Errorbar

    
.. image:: ../images/XPERIOR-Communicator-plot-histogram.jpg
    :width: 30 %
    :alt: Example 3 - Histogram

    
.. _macros:
    
Macros
------

Are user-defined procedures in form of python code. For a new macro definition, press ``Macro Setup`` button, as shown in the figure. All **Macro** declarations are stored locally under user's application path.

.. note:: It is a short script started in `shell`_ running in the main thread; therefore consider time-length of such procedure. 


You can also put instrument devices to the macro definition. Such devices are then hard-coded, statically defined. To create a single dynamic device, use *_device* string in your macro's source code. Depending on a selection in the **Instrument choice** control, that device will be used for communication.

Macro is started with mouse click on associated button with the standard output redirected to `shell`_. Macro can't be part of an automated script.

.. figure:: ../images/XPERIOR-Communicator-macro-setup.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Macro Setup - environment variables example


.. _debugger:

Debugger
--------

Starting a script with the ``Debug Run`` button prepares the script as a *debuggee server* to wait for external debugger (`WinPdb <http://winpdb.org/>`_).

Winpdb is a platform independent GPL Python debugger with support for multiple threads, namespace modification, embedded debugging, encrypted communication and is up to 20 times faster than pdb. *Created by Nir Aides, released in term of GNU General Public License version 2 or later.*

.. figure:: ../images/XPERIOR-Communicator-winpdb.jpg
    :align: left
    :figwidth: 100 %
    
    Figure: Xperior script in WinPdb Debugger

Features
********

* Flow control - breakpoints, conditional breakpoints, next, step into, jump, etc.
* Namespace analysis and modification - includes globals, locals, exceptions
* Multithread support - thread tracking & analysis
* Stack analysis - frames view with detailed information
* Commands Console 


How to setup the debugger
*************************

.. Warning:: Xperior needs to be restarted after debugging finishes.

1) Start a script with Debug Run button
2) In winpdb go to :menuselection:`File->Attach`
3) When prompting for a password, type "test"
4) In host: localhost, connect to filename: "communicators editor"
5) You can use the debugger now
6) important: restart the Xperior application after you finish debugging. Normal script start will not work otherwise.


Restrictions
************

* can't debug a script containing *execute_stop()* directive
* can't debug a script modifying system trace or profile (*sys.settrace*, *sys.setprofile* functions)
* can't debug XPERIOR application itself

.. _com_light:

Communicator Light
------------------

Is a console mode of Communicator enabling almost identical (see :ref:`com_limit`) execution of the test scripts. Benefits are compact distribution and no need of Python interpreter installation. Is distributed in form of an ``*.exe`` file + additional files. The generated **communicator-light.exe** file itself does not provide all Python modules. This means that some Python test scripts may fail because they need some functionality which is provided by a module which is not compiled into **communicator-light.exe**. To get the needed modules compiled into the executable, the needed python module(s) has/have to be imported within the *_modules.py* file prior the compilation.

To change the instrument and SOAP configuration, edit *instrument.init* and *soap.init* files respectively. They are located in :download:`../../../source/utilities/Communicator/dist` directory.

.. _com_limit:

Limitations
***********

* no GUI; with GUI connected commands 


How to build
************

* generate **communicator_light.exe**: :download:`../../../source/utilities/Communicator/setup.bat`
* configure instrument.init and soap.init accordingly
* test it!: :download:`../../../source/utilities/Communicator/dist/example.bat`


.. figure:: ../images/XPERIOR-Communicator_light-help.jpg
    
    Figure: communicator_light.exe
    
.. figure:: ../images/XPERIOR-Communicator_light-example.jpg

    Figure: communicator_light.exe - example of communication