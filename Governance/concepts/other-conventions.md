# Conventions specific to sub-domains and/or projects
We collect here other conventions which apply to sub-domains of climate science or specific
projects, if you know of more please let us know. 

## CMIP
* [CMOR - Climate Model Output Rewriter](https://cmor.llnl.gov)conventions and associated software used to generate CMIP model output. They also include rules around filenames and directory structure. 
* Their [variable name tables](https://github.com/PCMDI/cmip6-cmor-tables/tree/master/Tables) are often applied to other climate data too, as there is not yet a conventions around variable names.  
* CORDEX has similar [conventions](https://is-enes-data.github.io/cordex\_archive\_specifications.pdf) and [variable tables](https://is-enes-data.github.io/CORDEX\_variables\_requirement\_table.pdf).

## Land 
* [ALMA data exchange convention](https://www.lmd.jussieu.fr/\~polcher/ALMA/) the Assistance for Land-surface Modelling Activities group established conventions for land-surface schemes and their outputs.

## Ocean 
* [gridspec](https://arxiv.org/pdf/1911.08638.pdf) defined by GFDL in 2019 as a standard for Earth System Model grids to be included in the CF Conventions. It used for MOM5 and MOM6 grids. 
* [IMOS](http://content.aodn.org.au/Documents/IMOS/Conventions/IMOS_NetCDF_Conventions.pdf)
IMOS] has very specific extensions of the CF conventions for different kind of ocean observation data, which has to be used if you want to contribute data to their portal. 
* [OceanSITES Data Format](http://www.oceansites.org/docs/oceansites_data_format_reference_manual.pdf) - extension of CF Conventions standard for OceanSITES data 
* [ARGO netCDF conventions for data centers](http://www.argodatamgt.org/Media/Medias-Argo-Data-Management/Argo-documentation/General-documentation/Data-format)
* [PMEL-EPIC Conventions](https://www.pmel.noaa.gov/epic/document/convention.htm)
* [US NCEI NetCDF templates](https://www.ncei.noaa.gov/netcdf-templates) - these templates illustrate how to apply CF and ACDD conventions

## Atmosphere 
* [NCAR-RAF Conventions for Aircraft Data](http://www.eol.ucar.edu/raf/Software/netCDF.html)

## Other 
* [AMBER Trajectory Conventions](http://ambermd.org/netcdf/nctraj.xhtml) for molecular dynamics simulations.
* [CF Discrete Sampling Geometries Conventions](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.6/build/cf-conventions.html\#discrete-sampling-geometries) - CF for observational and point data 
* [COMODO](https://web.archive.org/web/20160417032300/http://pycomodo.forge.imag.fr/norm.html) ??? still used?
* [UGRID Conventions](http://ugrid-conventions.github.io/ugrid-conventions/) for unstructured (e.g. triangular, hex) grids. 
* [SGRID Conventions](http://sgrid.github.io/sgrid/) for staggered, structured (e.g. ROMS, WRF) grids 
* [UNIDATA NetCDF conventions lists](https://www.unidata.ucar.edu/software/netcdf/conventions.html) - including COARDS and other older conventions
