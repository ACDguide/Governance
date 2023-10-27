# New, modified, and derived datasets

## Creating new datasets from raw data

Creating netCDF files from scratch, using raw data (e.g., from a csv file or pandas array) can be tricky, however tools exist to aid this process.

Some tools that can be used to create netCDF files include:
- The Python netCDF4 API (https://unidata.github.io/netcdf4-python/), which allows for very granular control to build netCDF objects and write to disk.
- The command-line netCDF utilities 'ncdump' and 'ncgen' (https://docs.unidata.ucar.edu/nug/current/netcdf_utilities_guide.html), which uses the .cdl format (a ncdump output style file; example on previous page) to create netCDF files from human-readable templates.
- The command-line CDO software (https://code.mpimet.mpg.de/projects/cdo) that contains many operators for climate data, including the capability to write new files; however it is best used for analysis and operations such as regridding.
- The Python package Xarray (https://docs.xarray.dev/en/stable), which is quickly becoming the standard for large-scale  spatiotemporal data production due to its use of dask (parallel computing in Python), its ability to work between netCDF4 and [Zarr](https://zarr.readthedocs.io/en/stable/), and its vast array of operations. See [here](https://towardsdatascience.com/how-to-create-xarray-datasets-cf1859c95921) for a tutorial on creating netCDF4 files from pandas arrays.

Additional considerations when creating a climate dataset from scratch include:
- Consider chunking and compression (links to BigData?), which are best configured early in the process.
- Use the smallest number of dimensions as possible, so maintain clarity. If many similar dimensions are required, consider separating these out into multiple datasets under a single collection.
- Use descriptive names for variables early on to avoid confusion later. Applying conventions (e.g. CF, ACDD) where possible can also help to ensure that variable information is not lost throughout the project.
- Always include units!
- Including descriptive global attributes (or an associated metadata file) from the start (even if it is very rough information saved in a general 'comment' attribute) can help to keep track of workflows and avoid loss of context information over time.

----------

Paola (new comments following meeting Sep23):

We discussed here mentioning tools to generate/modify a netcdf file (ncdump/ncgen, nco to modify attributes, how xarray/matlab "create" netcdf file)
rather than trying to re-create every possible workflow.
As well as things a user should check to make sure they're following the reccomendations listed in create-basics. For example ar ethe attributes still relevant both at global and variable level?


Paola:  



at initial level some global attributes/metadata associate file to keep track of workflow and describe what's in the file.

Chloe:  
Provenance: https://acdguide.github.io/Governance/concepts/provenance.html

Link to ACCESS Archiver

## Modifying existing files in-situ
ncatted, etc

history updating; Damien's command-line provenance tool; keepattrs; etc

## Creating derived datasets from existing/published data

Paola:  
Make sure original attributes/documentation are still relevant

be careful particularly with units, cell_methods and coordinates that might have changed

Chloe:  
Provenance: https://acdguide.github.io/Governance/concepts/provenance.html
