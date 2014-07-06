.. _userTutorialsDataOrganization:

Keeping Data Organized
======================

Keeping your data well-organized and annotated is crucial to ensuring that data will be
interpretable and analyzable in the future.

This tutorial describes the recommended practices for organizing data with ACQ4 using a simple example experiment.
Also see
:ref:`Data Folders<userModulesFolders>`.

Folders are named using the naming rule specified in the configuration for that folder type,
followed by a numerical identifier "_XXX" that increments to avoid creating duplicate names.

For example, suppose we define three folder types for storing data in slice electrophysiology experiments:
'Day', 'Slice', and 'Cell'. For each Day, there will be one or more Slices,
and for each Slice there will be one or more Cells. If we create new
folders in the following order: [Day, Slice, Cell, Cell, Slice, Cell, Cell], then they
will be automatically organized into the following structure:

    Day/
        Slice_000/
            Cell_000/
            Cell_001/
        Slice_001/
            Cell_000/
            Cell_001/

Thus, typically at the start of an experiment, you will create a *Day* with the Data Manager. There are multiple fields
that can be populated at this point, and you should take a few minutes to fill them out completely. It is also
very helpful later on if you can fill these fields out consistently across days. For example if the ACSF is "standard",
then state "standard ACSF" every time. Then if you use a modified ACSF (for example, with more physiological divalent
solutions than normally used for slice experiments, e.g., 0.8 mM Mg and 1.0 mM Ca), you should state "ACSF: 1.0 Ca, 0.8 Mg"
and provide a detailed recipe (or a pointer to where the recipe can be found) in your lab notebook.

Next, as you load a slice into the recording chamber, you will create a new *Slice* entry. Each *Slice* entry also
has a field that you can fill out (in the Data Manager, "Info" tab) to provide information about the slice.

Finally, as you patch a cell, you
will create a new *Cell* entry. Again, the *Cell* entry has a field in the Data Manager than can be filled out to provide
information specific to that cell. Often as you work with a *Cell*, it will be useful to keep this window available to enter
new notes and observations as you run different protocols.

Acq4 will automatically number the *Slices* and *Cells* as the day progresses; you should
not try to change this numbering. If you
exit the program or the program crashes, you **MUST** use the DataManager window to reset the program so that it points
to the right level of the structure.

**Warning**: *If the intended file organization becomes disrupted, such as happens after a program crash when you forget
to reset the directories in the Data Manager, do not use the Windows Explorer
or OSX File Manager to move the files and directories around!* ACQ4 generates metadata files that are
held in a text format in hidden files in every directory (named ".index"). Because these are invisible most of the
time, they may not get copied correctly, and it is very likely that you will lose important information that will be needed later
to properly analyze the data later. Instead, use the left hand pane in the Data Manager
window to do the reorganization; the Data Manager will take care of copying the data and the associated .index files to their proper locations.



About Data Notebooks
--------------------

Although keeping the records electronically is nice, it is not a complete substitute for the paper laboratory notebook. The
notebook needs to also contain information about the experiments, as a kind of metadata, that completes the information
you enter into the program. The best practice is to write an entry for each cell recorded, including
the protocols run and where the data is stored in the data notebook, and to have complete information about the solutions used
or other factors that are needed to reproduce the experiment. If you say that the electrode is "Cs", later you will want
to know which Cs solution was used. Did it have low or high Cl-? Was the major anion MethaneSulfonate or gluconate? Did you put
a dye in it, and if so how much? How old was it?


