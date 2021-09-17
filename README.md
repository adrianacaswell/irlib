[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.439723.svg)](https://doi.org/10.5281/zenodo.439723)
TODO - refresh DOI for new version

*Radar Tools* is a library and set of tools useful for visualizing and
processing data collected from ice-penetrating radar. The tools have been
designed to work the HDF5 datasets generated by [Blue
System](http://www.radar.bluesystem.ca/) IceRadar.

There are two primary ways of using *Radar Tools*. The first is to use the
command-line and graphical tools, listed below. These tools provide an
efficient and simple way to apply established methodologies for analysing radar
data. Pre-written filters and processing routines are called by typing
commands.

![](http://njwilson23.github.com/radar_tools/images/repo_image.png)

The second way is to use the ``irlib`` package through custom Python scripts.
This makes it possible to programmatically analyze radar data. New filters and
processing routines can be implemented using the API.

There is experimental support for reading other types of datasets using *Radar
Tools*. Right now, it's possible to read CReSIS and pulseEKKO PRO lines, making
the filters in ``irlib`` available. Helper functions to load CReSIS \*.mat files
and pulseEKKO PRO \*.HD and \*.DT1 files are in ``itools.py``

Graphical tools:
----------------

- **icepick2**: View radar lines directly and experiment interactively with
  processing filters. Pick reflection arrivals from a radar line, either
  manually or with simple pattern recognition

- **icerate**: Rate reflection quality using **icepick** output


Command-line tools:
-------------------

- **h5_dumpmeta**: Dump metadata from an HDF5 survey into a CSV or shapefile
- **h5_replace_gps**: Replace the coordinates in an HDF5 survey with those from
  a GPS eXchange (GPX) file or an NRCan PPP csv 
- **h5_add_utm**: Add UTM coordinates to an HDF5 survey file 
- **h5_generate_cache**: Generate caches to speed loading radar lines (and do some cleaning steps)
- **h52a**: Export a line from an HDF5 file to ASCII or binary for use in other software (like Reflex)
- **antenna_spacing**: Reads CSV from h5_dumpmeta and creates an offsets file with antenna spacing
- **join_radar**: Takes picked-, rated- and offset files and calculates ice thickness
- **merge_picks**: Brings old picks into sync with a new picking project
- **plottrace**: Plot a radar trace acquired at a single location
- **plotline**: Plot a radar section along a line of locations

Dependencies:
-------------

*Radar Tools* is compatible with Python 3 (tested under 3.8). It should work under Windows, OS X, 
and Linux.  To install it, conda is recommended to manage the environment and dependencies. 
Specific steps are in the documentation pdf.  


Documentation:
-------------
Full documentaion is generated with sphinx and is available ![here](http://njwilson23.github.com/radar_tools/irlib_documenation.pdf)

Change Log: 
------------------

*irlib 0.5* changes include the following: 
- conda environment defined for easy installation
- replaced shebang for all scripts with /usr/bin/env so that it would work with conda
- works in Python 3, Python 2 compatibility hopefully preserved (but not tested)
- compatible with newer versions of h5py, StringIO
- uses argparse library for commandline options - To get the syntax message type the file with flag -h and it will show up. 
- compatible with various flavours of the BlueSystems IEI software - see documentation pdf for more details
- h5_dumpmeta.py - added extra metada fields, sorts on FID, option to create a shapefile output (points or lines or both)
- h5_add_utm.py - works with new lat/lon format 
- h5_replace_gps.py - improved argument handling, enhanced support of ppp files, can offset elevation
- h52a - added format that can be read by REFLEX (not well tested)
- antenna_spacing.py - made output file naming a bit more robust
- join_radar.py - rewritten to optionally circumvent need for offset and rating files, added option to create shapefile
- merge _picks.py - added this to reuse old picks with re-cleaned data
- reorganized the documentation and added suggested workflows

*irlib 0.4* represents significant refactoring and cleaning of both the library
and application design. Breaking changes in the final version will be kept to a
minimum, however the *stable-0.3* branch is available if necessary.

- remove deprecated `CutSingle`, `CutRegion` methods
- refactor pickable gathers into separate subclasses
- map window
- refactor icepick, irview, icerate into a single codebase, kept in `irlib/app/`
  (all except icerate)
- build *icepick2* based on the refactored `app` codebase
- modular command system, one of the benefits of which is that additional custom
  filters can be added easily at runtime and on a project-basis
- rewrite ``h5_replace_gps`` to be more robust, handle timezones, and work over
  multiple days
- some bug fixes and polishing
- Python 3 compatibility (WIP: tests pass, basic icepick2 use)
- project config file (not complete)
- composable line gathers and surveys by overloading arithmetic operators?
- HDF file write?
- PulseEkko data reader?


*irlib 0.3* this is a stable branch. 
TODO - Nat do you have anything to say here? 


License:
--------

*Radar Tools* is provided "as is," without any warranty. Some parts of
*Radar Tools* are affected by different licensing terms. See `license.txt` for
detailed information.

