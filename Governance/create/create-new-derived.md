# New, modified, and derived datasets

## Creating new datasets from raw data
Paola (new comments following meeting Sep23):

We discussed here mentioning tools to generate/modify a netcdf file (ncdump/ncgen, nco to modify attributes, how xarray/matlab "create" netcdf file))
rather than trying to re-create every possible workflow.
As well as things a user should check to make sure they're following the reccomendations listed in create-basics. For example ar ethe attributes still relevant both at global and variable level?


Paola:  
however rare, we could cover starting from a template, as for a cdl file (i.e. a ncdump output style file)

data saved from analysis - start saving data with reasonable default format (free, common etc.) and chunking, compression etc if netcdf

the least complicated possible dimensions, keeping into account also data use rather than dumping everything as it is

introduce early descriptive names for variables, and conventions where applicable

include units if applicable

at initial level some global attributes/metadata associate file to keep track of workflow and describe what's in the file.

Chloe:  
Provenance: https://acdguide.github.io/Governance/concepts/provenance.html

Link to ACCESS Archiver

## Modifying existing files in-situ
ncatted, etc

## Creating derived datasets from existing/published data

Paola:  
Make sure original attributes/documentation are still relevant

be careful particularly with units, cell_methods and coordinates that might have changed

Chloe:  
Provenance: https://acdguide.github.io/Governance/concepts/provenance.html
