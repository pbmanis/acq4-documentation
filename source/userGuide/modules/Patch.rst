.. _userModulesPatch:

The Patch Module
================

This module is used to assist in patching cells and to monitor cell health throughout the experiment. It provides a few basic functions:
    
* Emits small current (ic mode) or voltage (vc mode) pulses repeatedly and estimates the input resistance and access resistance to the electrode or patched neuron.
* Can periodically monitor the cell's status after patching. It is expected that a Patch module may be running concurrently with other modules making use of the same hardware; in this case the modules are automatically synchronizes to avoid resource collisions.
* Plots estimates of input resistance, access resistance, holding values, and capacitance over time. This aids the experimenter in seeing the effects of manipulations on seal resistance, access resistance, and the general health of the cell over the course of the experiment.
* Stores a record of estimate data as it is collected (Note that the Patch module currently does *not* store raw recording data)

.. figure:: images/patch.png
    :align: center

The patch module acquires data from a single patch clamp device, which is specified in the :ref:`modules section <userConfigurationModules>` of the configuration file. The following example configuration defines *two* different patch module instances, each of which will use a different clamp device::

    modules:
        Patch 1:
            module: 'Patch'
            config:
                clampDev: 'Clamp1'
        Patch 2:
            module: 'Patch'
            config:
                clampDev: 'Clamp2'

For an example of a typical patch experiment using this module, see the :ref:`patching tutorial <userTutorialsPatching>`.


Stimulus Controls
-----------------

When the Patch module is running, it repeatedly outputs a square pulse waveform to the patch clamp amplifier while recording from its electrode signal. The clamp mode, pulse shape, and timing are all configured in the set of controls labeled "Stimulus control" in the figure above.

* **VC/IC** radio buttons set the recording mode of the amplifier to voltage clamp or current clamp, respectively. Note that the amplifier's mode will not change until immediately before a recording is about to be made.
* **Pulse** check boxes determine whether a square pulse should be present in the stimulus waveform, while the adjacent spin boxes select the amplitude of the pulse.
* **Hold** check boxes determine whether any holding potential or current is applied, and the adjacent spin boxes select the value. 
* **Delay Length** sets the amount of time in the stimulus waveform before and after the square pulse.
* **Pulse Length** sets the duration of the square pulse in the stimulus waveform.
* **Cycle Time** sets the desired amount of time from between the onset of consecutive recordings.
* **Average** sets the number of pulse recordings to average together before displaying and analyzing the result.

Typically, the experimenter will want to change these settings multiple times over the course of patching a cell. For convenience, there are four buttons which immediately apply pre-set values to the stimulus controls described above:
    
* **Bath** is used to measure the electrode resistance while the electrode is in the bath, away from a cell.
    * Mode = VC
    * Holding = disabled
    * Pulse = enabled (default amplitude is -10 mV)
    * Delay Length = 10 ms
    * Pulse Length = 10 ms
    * Cycle Time = 200 ms
    * Averages = 1
* **Patch** is used to measure the seal resistance while the electrode is forming a gigaohm seal. It may also be used to measure the input and access resistance of the cell after rupturing the cell membrane.
    * Mode = VC
    * Holding = enabled (default is -65 mV)
    * Pulse = enabled (default amplitude is -10 mV)
    * Delay Length = 10 ms
    * Pulse Length = 10 ms
    * Cycle Time = 200 ms
    * Averages = 1
* **Cell** is a current-clamp pulse used to measure the state of the cell.
    * Mode = IC
    * Pulse = enabled (default amplitude is -30 pA)
    * Delay Length = 30 ms
    * Pulse Length = 150 ms
    * Cycle Time = 250 ms
    * Averages = 1
* **Monitor** is used to periodically monitor the health of the cell and status of the access resistance during the course of an experiment.
    * Cycle Time = 40 s
    * Averages = 5

To begin recording, click the **Start** button. The command waveform and electrode recording signals are displayed in the right-side panels. Any of the settings described above may be changed at any time during the experiment. 


Parameter Measurements
----------------------

For each recording, the Patch module calculates the access resistance, input resistance, resting membrane potential (or holding current), and cell capacitance [1]_


The software automatically calculates a fit to the trace collected in each of the modes. From this fit it calulates 
parameters of the cell, electrode or patch. By default the fit that is calculated is displayed with the patch recording 
as a blue line. To speed things up you can turn off the drawing of this fit by unchecking Draw Fit. If you do this the 
fit and parameters will still be calculated, just not drawn.

All of the parameters will be calulated (and saved if record is pressed). You can plot one or more of the parameters in the
bottom plot window by selecting the check box next to the parameter. You can reset the plot by clicking Reset History. Whenever
you press record, data for all the time that is in the plot window is saved, and incoming data is also saved. 

.. [1] Santos-Sacchi, 1993. Voltage-dependent Ionic Conductances of Type I Spiral Ganglion Cells from the Guinea Pig Inner Ear. J Neurosci. 1993 Aug;13(8)


