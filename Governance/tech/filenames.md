## Naming
You can use your filenames to include information, here is some you can consider:

* project, simulation and/or experiment acronyms, you might have to use a combination of them.
* spatial coverage: the region or coordinates range covered by the data, could also be a specific domain for climate model data, i.e. ocean, land etc.
* grid: could be either a grid label or spatial resolution
* temporal coverage: a specific year/date or a temporal range
* temporal frequency: monthly, daily etc
* type of data: again this depends on context, if the same directory contains data from different instrumentations it is important to specify the instrument in the name. For coupled model output this could be the model component, if you are using one file per variable the variable name.
* version: this is really important if you are sharing the data even if only 1 version exists at the time
* correct file extension

## Tips for machine-readable files
* avoid special characters: ~ ! @ # $ % ^ & * ( ) ` ; < > ? , [ ] { } ‘ “
* do not use spaces to separate words use underscores "_" or dashes "-" or CamelCase
* use YYYYMMDD for dates, it will sort your files in chronological order, absolutely avoid "Jan, Feb, .." for months as they are much harder to code for.
* or number sequence use leading zeros: so 001, 002, 020, 103  rather than 1, 2,.. 20, .. 103
* try to avoid overly long names, for a single file, directory keep it under 255 characters, for paths 30000.
* avoid having a large number of files in a single directory … but also an excessive number of directories with one file each
* always include file extension, some software can recognise files from their header, but this is not always the case

### Online Resources
We partially based this page on the resources listed below, we recommend to check them for more insight and advice.

* [Best practice to organise your data](https://www.earthdatascience.org/courses/intro-to-earth-data-science/open-reproducible-science/get-started-open-reproducible-science/best-practices-for-organizing-open-reproducible-science/) - part of an Open reproducible science course from the University of Colorado 
* [Software Carpentry video covering DRS best practices](https://youtu.be/3MEJ38BO6Mo)
* [Best file naming practice handout (pdf) from Standford University](https://stanford.box.com/shared/static/yl5a04udc7hff6a61rc0egmed8xol5yd.pdf) 
