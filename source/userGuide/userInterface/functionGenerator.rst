Function generators
===================

Many situations in ACQ4 ask the user to define a waveform that will be sent to an analog or digital channel on a :ref:`DAQ device <userDevicesNiDAQ>`. For this purpose, ACQ4 uses a general-purpose function generator control accompanied by a plot displaying the output of the generator:

.. figure:: images/functionGenerator1.png

Function generators have two modes of operation: *simple* and *advanced*. The simple mode allows the construction of waveforms by selecting one or more elements to add to the waveform and adjusting the parameters for each element. 

.. figure:: images/functionGenerator2.png

Function generators are also used to design sequences of waveforms with one or more parameters that vary for each point in the sequence. In simple mode, each of the paraneters that define a waveform element may be expanded to reveal a set of sequencing controls that determine whether and how a parameter should be handled in a sequence:

.. figure:: images/functionGenerator3.png

The advanced mode allows the user to enter a Python expression that will be evaluated to yield the waveform output:

.. figure:: images/functionGenerator4.png

[Note about units]

[Note about the major differences between simple and advanced mode]
