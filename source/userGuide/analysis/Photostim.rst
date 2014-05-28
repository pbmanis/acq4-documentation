<<<<<<< HEAD
===============================
Photostim Module (Analysis)
===============================

.. index:: PhotoStim, mapping, uncaging, ChR2

This is a brief tutorial on using the PhotoStim module to analyze uncaging or 
photostimulation data. 

Open *Acq4*, and load the Data Manager. Point the Data Manager at to top level directory 
for your data (for example, to the disk or the folder holding your data), using the 
*Top-Level Directory* button. Next, select (or create) a Database using the Database 
functions (Open, Create). You should have a database open to use the PhotoStim module. 
Next, select the date for the experiment in the left pane.

Now you can open the analysis module with *Load -> Photostim*. This will bring up the
module window. The window has 4 sections, divided by splitters. Each section has clickable
*tabs* (although they do not have a typical tab appearance) across the top; each tab
displays different information. You may drag the tabs around on the window as well to
reorganize them to suit your needs. 

File Loader
-------------
Use this tab to pick up the subfolders containing the relevant data sets
from the directory you have selected
in the Data Manager. These subfolders will usually be named *slice_000*, etc. 
Open one of the subfolders by clicking on
the triangle to the left of the name to expand an entry. Repeat this to select cells for
the slice and date, and for a given cell, to show the 
protocols that were run as well as some of the files (for example, images) that are
stored in that directory. You can then select a map protocol (single click; you do not
need to *open* it), and
click on the *Load File->* button below the File Loader to bring the data into the program.
When the data is loaded, 
there should be a set of spots in the *Canvas* window, corrsponding to the targets sampled
by the scanner during the experiment. If there are no spots, check the log for errors, and
also click the *Auto Range* button to the right of the Canvas (see below) to rescale the 
view. 

Database
---------
To the right of the *File Loader* tab is the *Database* tab. This is a bit experimental,
and requires some care in use. It is will not be described here.

Canvas
-------
To the right of the central display splitter are the *Canvas* and *Scatter Plot* tabs.

Go to the Canvas tab. If there is no pane on the right, click the *>* in the upper right
corner to  show the control pane. This pane provides the following functions:

	*Store SVG* and *Store PNG* allow you to save the current Canvas image as a file. 

	*Auto Range* will bring all of the elements displayed in the Canvas 
	 onto the window. This may be useful if you have expanded the window, 
	 or if you have maps that are in different positions so that they are not all
	 visible when they are brought in. 

	*Redirect*, and the drop list next to it: I don't know what these do. 

Below this is a list of the items currently available for display. 
You can check or uncheck these to show or hide them.
For some operations, you may need to select one of these (rather than just check it) to
make the program operate on a specific item. 

Normally at this point you will go to the Detection Opts and Map Opts tabs for the next 
steps. 

Detection Opts: 
----------------

This window shows the parameters for the currently loaded *FlowChart*. The default
flowchart, *default.fc*, does simple event detection by deconvolution, and provides
a number of relevant measurements on detected events.
The *Load*, *Save*, and *As..* buttons allow you to load a new
flowchart, or save the current flowchart with new parameters, or *save as* with a new name.

Flowchart
----------
The *Flowchart* button on the bottom brings up a new window with 
the current flowchart. 
Each part of the flowchart has parameters, and also has a *[X]* box. The *[X]* box, when checked,
is green, and this means that the particular step in the analysis is skipped (e.g., the
output is equal to the input.). 

You will use the *Detection Opts* tab to change the parameters for event detection. But,
first, let's display a trace.

Click on one of the spots on the map. In the *Data Plot* on the right, under the map, you
should see a trace. The trace may have detected events (indicated by a blue line that
is superimposed on the white data trace). The goal of setting the parameters in the detection
section is to optimize event detection, reject noise, and be sure that you are looking at
the right aspect of the data. Use the *PreRegion*, *DirectRegion* and *PostRegion* options
to set the analysis windows appropriate for your data.
Use the *Threshold* options to adjust the sensitivity of the
analysis. Check several traces to be sure you agree with the results. 

To help set the threshold, click on the *Filter Plot* tab under the *Data Plot*. Watch the units,
and set the *Threshold* to a value that allows this plot to discriminate events from noise. You 
may need to change the settings of the *ExpDeconvolve* function in the Detection Options
to get consistent event detection. Use the *Event Table* tab to examine the results 
of the measurements
on the individual events (remember to scroll it horizontally - there is more information
than will fit on the screen). Once you are comfortable with these, *Save* the parameters 
in the *Detection Opts* tab, then select the *Map Opts* tab.
 
Map options
------------
The *Map Options* determine how the analysis results are displayed on the map in the Canvas. 
This section has a number of variables that you can control, so some experimentation is
necessary to achieve a useful display.
Note that the *Map Opts* has it's own independent Flowchart (default.fc). Use the *Load*
list to select a parameter type to display, for example *FitAmpEx*, which means *fit
amplitude excitatory*. These would be the amplitudes of the deconvoluted data peaks. 
In the box below the *Color scheme*, there are 3 rows. These indicate what is plotted (
the *arg*), how it is applied (added or multiplied), the data range that will be 
represented by the color scale, and then the color scale itself. In this case, with the
default flowchart, you will have *fitAmplitude_PostRegion_sum* (look at the *Stats* tab
below the data plot if you want to know what the value is for the current trace). The value
of this variable
is added to the current display 
(and since it is the first one, it is added to a map of zeros), with a range. 
Next is the *PostScore*, which is calculated as the event rate during the PostRegion
time window, minus the event rate during the PreRegion window. Thus, one event in a 100
msec window will have a score of 10 (1 event / 0.1 seconds). 
It may be useful to adjust the slider to help show
rarer events. Below this is the *DirScore*, which is the score for events in the *Direct*
window that you defined in the Map Opts. These would be events where either the latency
of the response was too short to be mediated synaptically (in the case of uncaging), or where
an event might have happened right before the stimulus. You can define this in different
ways. In any case, this will be (in the default settings) a white color that is added
to the spot, indicating that the response may
have been affected by ongoing activity or direct stimulation. 

To display the results on the map, press the *Recolor* button. If this is the first time
you have colored the map, it may take a few minutes to calculate all the responses. A progress
bar will appear. If you do not change the analysis parameters (so that the data results
are the same), but just recolor the spots in the Color scheme, the progress will go
much quicker. 

Changing the colors:
--------------------

The color controls consist of a color bar with 2 or more triangular
controls. Dragging the controls changes the color scale (the minimum data level is plotted
as the left-most color, the maximum data level is plotted as the right-most color). Single
clicking
beneath the color bar will add a control point. Single clicking on the control point will
bring up a color control widget that allows you to set the color for that control point.
Control-clicking on the triangle removes the color and it's control point. Hitting *Recolor*
will change the map color scheme according to the color controls.  
With this system, you can create colors any way you wish.

Superimposing maps and images:
------------------------------

Now that you have a map that is to your liking, it might
be time to put it over an image of the slice. Go to *File Loader*, and select the image (it
might be a "tiff" image). The image will initially be placed on top of your map and
might hide it.  However by adjusting 
the order and the *Alpha* in the panel to the right of the Canvas, you can make the image
appear as it should (e.g., behind the map, and giving the map some tranparency so that
the image shows through a bit. To reorder the images (think of them as being in layers like
in Photoshop, or in a stack), select the image in the list of displayed items
on the Canvas, and
drag it so that it is placed lower in the list. The image now will appear behind the map. You
may wish to select the map and change it's Alpha to better blend the two representations. 






=======
Photostimulation Mapping
========================
>>>>>>> 34fd7f9961086e3ec881be19ddd3ebd8e37d077d
