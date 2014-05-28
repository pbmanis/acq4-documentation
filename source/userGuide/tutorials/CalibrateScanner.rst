.. _userTutorialsCalibrateScanner:

Calibrate Scanning Mirrors
==========================

Overview
--------

The scanning mirror positions are calibrated against the Microscope (stage reference) using an automated method. Calibration requires
 a fluorescent target, and a system that has been optically aligned so that the laser beam is visible on a target underneath the objective.
The calibration changes with each objective used, or if an objective is removed and reattached, so frequent calibrations are recommended.
The current calibration can also be checked with a simple Task set up in the :ref:`Task Runner<userModulesTaskRunner>`.

.. _userTutorialsCalibrateScannerDailyCalibration:

Daily Calibration Steps
-----------------------

#. In the :ref:`Manager Device window<userModulesManagerDevices>`, select the Scanner device (not "Scanner Raw").
   Set the objective if it is not automatically determined.
#. Open the :ref:`Camera module<userModulesCamera>`, start the camera, and manually open the laser shutter to make sure the laser
   is in-focus. Fluorescent targets can be made from a piece of yellow laboratory tape (for a blue laser), a red plastic for a multiphoton
   laser, or a piece of nitrocellulose paper soaked in a fluorescent dye, dried, and sandwiched between two small coverslips.
#. Set Camera to “CLEAR_MODE” = clear pre-exposure, and set binning to 4 (or whatever is needed to get high frame rate, around 30 fps).
#. If the laser is out of the view of the objective, you may need to adjust the X and Y voltages on the
   Scanner-Raw device in the :ref:`Manager device window<userModulesManagerDevices>` (see step 3 below).
#. Close the laser shutter, and make confirm that the correct objective is selected in the :ref:`Manager Device window<userModulesManagerDevices>`.
#. Click “Calibrate” (:ref:`Manager device window<userModulesManagerDevices>`, Scanner device). Pay close attention to the image showing the spots that were detected during the calibration (if no spots were detected at all, you may need to reconfigure the calibration routine; see below).

    a. Do the spots cover the entire region you wish to use for photostimulation? If there are large regions with dim or absent spots, your objective might need to be cleaned. If the spots suddenly cut off at a flat edge, then you may need to adjust the XY scan ranges (see below).
    b. Are the spots round over the region you want to use for photostimulation, or are there NO spherical aberrations (looks like the spots have tails)? If the spots are elliptical or have aberrations, then you may need to realign the scanning system. (Note: as it is currently configured, the 'sweet spot' where the laser is focused perfectly is currently NOT exactly in the center of the view).

#. Repeat steps 1-5 for any other objectives you wish to use.

You can test the calibration by opening "scanner_test" in the :ref:`Task Runner<userModulesTaskRunner>`.
 When this protocol is running, the laser should track the pink circle drawn in the camera module.


.. _userTutorialsCalibrationScannerInitialCalibration:

Initial Calibration
-------------------

These steps are for new systems, or if things go terribly wrong:

#. Determine the 'center' voltage values for the scan mirrors (step 3 below)
#. Look at the "Calibration Parameters" box for the scanner in the :ref:`Manager device window<userModulesManagerDevices>`. Select the correct camera and laser pair you wish to calibrate.
#. Make sure that the XY scan ranges cover ~2V on either side of the center values.
   (For example, if the center X voltage is -0.4, then "X min" should be about -1.4 and "X max" should be about 0.6)
#. Decide on a suitable set of parameters for the camera to use during the calibration.

    a. The exposure time should be short (~1ms) so that the spots appear to be stationary in each frame.
    b. The image should be bright enough to clearly distinguish the spot from background noise (increase
       binning to decrease noise)
    c. The frame rate should be fast enough to catch a large number of spots (~30fps). Increase the binning
       to get a faster frame rate, or select a smaller ROI if you know you won't be using the entire field of view (this is generally true for the Retiga cameras).
    d. The image resolution should be high enough to clearly determine the center of the spot (usually this is not
       a problem, even with high binning)
    e. If it seems the camera is not capable of meeting these criteria, you can make the scan duration longer
       or find a way to get more light through the scope

#. Click "Store Camera Config" (in :ref:`Manager device window<userModulesManagerDevices>`) to store the current settings.
   These settings will be restored every time a calibration is run.


.. _userTutorialsCalibrateScannerOpticalAlignment:

Optical Alignment (This should be rarely needed, once the optical train has been set up and aligned, but may need attention if
you cannot ):

#. Do steps 1,2,3 above (:ref:`Initial Calibration<userTutorialsCalibrationScannerInitialCalibration>`) as if preparing for calibration.
#. Place a laser target (pinhole in the cage between the dichroic cube and the first scan lens (the lens closest to the scan mirrors).
#. Adjust the X, Y values for the Scanner-raw device (in the :ref:`Manager device window<userModulesManagerDevices>`) until the laser hits the center of the target. The current values are the "center" values for the scan mirrors, and in general will not be 0,0.
#. Remove the target, and check the position of the spot as seen by the camera. If the spot is significantly off-center, then adjust the angle of the dichroic mirror. Do this CAREFULLY since the dichroic can be broken if the angle is pushed too far.
#. Recalibrate using the :ref:`Daily Calibration<userTutorialsCalibrationScannerDailyCalibration>`.

