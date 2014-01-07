Function generators
===================

Many situations in ACQ4 ask the user to define a waveform that will be sent to an analog or digital channel on a :ref:`DAQ device <userDevicesNiDAQ>`. For this purpose, ACQ4 uses a general-purpose function generator control accompanied by a plot displaying the output of the generator:

    .. figure:: images/functionGenerator1.png

Function generators have two modes of operation: 
    
* **Simple mode** The simple mode allows the construction of waveforms by selecting one or more elements to add to the waveform and adjusting the parameters for each element. This mode is rather limited in its capabilities (currently, the output may be the sume of one or more square pulses or pulse trains), but is simple to use and generates a metadata structure that can be easily parsed by analysis software.
* **Advanced mode** allows the user to enter a Python expression that will be evaluated to yield the waveform output. This mode is far more flexible in the types of waveform it can generate, but requires some minimal knowledge of the Python language. In some cases, it also presents a difficult analysis problem because a single waveform may be specified in many different ways. The result is that analysis software may be required to either parse complex Python statements or directly analyze the waveform to determine the stimulation parameters used.

Simple mode
-----------

    .. figure:: images/functionGenerator2.png

Waveform sequences
------------------

Function generators are also used to design sequences of waveforms with one or more parameters that vary for each point in the sequence. In simple mode, each of the paraneters that define a waveform element may be expanded to reveal a set of sequencing controls that determine whether and how a parameter should be handled in a sequence:

    .. figure:: images/functionGenerator3.png

Advanced mode
-------------

    .. figure:: images/functionGenerator4.png

[Note about units]

[Note about the major differences between simple and advanced mode]
