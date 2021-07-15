Data conventions and standards are an important tool to manage your data
in a way it can be easily and effectively shared with others.
Conventions help achieving this in two ways: 
* formatting the data in a
way which is easy for others in the same community to use; 
* providing enough information about the data (metadata) in a shared "language" so
others can understand the data as it was meant to by its creator
Conventions are also convenient for anyone using them, as they provide
and easy to adopt template for your data and you do not need to invent a
new data model with every new project. What's more they help you being
consistent, and you are less likely to mis-interpret your own data later
on. Some conventions are universally adopted as the metric unit system,
and we all use them without even noticing anymore. Others are community
specific and are developed to tackle specific data formats and needs of
a scientific discipline. To read more about why data standards are
important there is this [https://ardc.edu.au/resources/community-endorsed-data-standards/
article from the ARDC]. The climate research community uses mostly [https://www.unidata.ucar.edu/software/netcdf/ NetCDF] (Network Common
Data Format) as a data format. NetCDF is a self-describing binary format
which means that metadata information is stored with the data
itself. The Climate and Forecast Conventions (CF Conventions) were
developed to standardised this metadata. 

### **CF Conventions**
The [https://cfconventions.org CF conventions] are specifically designed
to facilitate the processing and sharing of NetCDF files. They are based
on the older [https://ferret.pmel.noaa.gov/noaa\_coop/coop\_cdf\_profile.html
COARDS conventions], which they extend. The first version (v1.0) of the
CF Conventions was released in 2003, the current version (in 2021) is
v1.8. Each new version tries, as much as possible, to be compatible with
older versions. The first versions, as the name implied were focusing on
climate and forecast data, since then they broaden their scope to earth
data in general, including observational data. CF is now widely adopted
as the main standard both in the production of NetCDF related code and
for the publication of NetCDF data. As the initial focus was to allow
interoperability of NetCDF based software packages, the conventions main
aim is to define clearly each variable and the spatial and temporal
properties of the data. Applying these Conventions to your NetCDF files
makes them more re-usable.  Most software used in Climate science will
know how to open and process correctly the files. The metadata
required will describe clearly the characteristic of the data in the
files, making it easier to identify correctly the variables and compare
them to similar data. CF Conventions focus mostly on the variable and
dimensions description, the full Conventions document is quite long but,
in most cases, you will be using the same attributes. This [https://climate-cms.org/2018/10/26/Setting-up-NetCDF-file-attributes.html CMS Blog] provides an example on how to apply them to your data,
covering the attributes most commonly required. Important elements of
the Conventions are: 
* the [https://ncics.org/portfolio/other-resources/udunits2/? UDUNITS2]
packages for units' standards 
* the [https://cfconventions.org/Data/cf-standard-names/77/build/cf-standard-name-table.html
standard\_name] whose scope is to provide a common terminology for
variables names. For example, every variable with the standard\_name
**''air\_temperature**'' can be defined as "''Air temperature is the
bulk temperature of the air, not the surface (skin) temperature.''" with
K or equivalent units, regardless of the way the actual variable is
named in the file. Standard\_name is a very useful attribute but should
be applied with attention. It is better to leave it out if a suitable
one is not available. There are various tools available to help you
check your files against a version of the CF Conventions. We covered
some in this wiki page: \[\[CF\_checker|CF checker]]   

### **Attribute Convention for Data Discovery**
The [https://wiki.esipfed.org/Attribute\_Convention\_for\_Data\_Discovery\_1-3
Attribute Convention for Data Discovery] covers mostly global
attributes which are used to correctly describe shared and published
data and to increase its discoverability in data portals. CF conventions
recommends only 6 global attributes to define the file content. ACDD
extends these to include all the information related to the publication
of a dataset, adding attributes like: doi, keywords, creator, publisher,
etc. The ACDD divides the attributes in three groups: 
* highly recommend - which can be define for any dataset (as 'title') 
* recommend - including attributes that should be define if existing (as
'id' for the DOI) 
* suggested - to further clarify the content but not critical 

When publishing several files as part of the same dataset these
attributes should all share the same values, as attributes like "title"
should define the "title" of the dataset not of the file itself. When we
publish data with NCI, which requires both CF and ACDD conventions to be
applied, we generate these attributes based on a DMP compiled by the
user. The CF checker linked above can also be used to check against the
ACDD conventions. Finally, conventions are useful only if the file
creator provide the correct values. When you generate a new file from an
existing one, the new file will inherit its attributes. It is up to you
to make sure they are still valid. If you want to preserve some of the
information from the original file, you can change the attribute name by
using a suffix as "source\_"  or "original\_" , so as to clarify they
apply to the source file not to the current version.

### **Conventions specific to sub-domains and/or projects**
We collect here other conventions which apply to sub-domains of climate science or specific
projects, if you know of more please let us know. 

#### **CMIP**
* [https://cmor.llnl.gov CMOR - Climate Model Output
Rewriter] convetions and associated software used to generate CMIP
model output. They also include rules around filenames and directory
structure. 
* Their [https://github.com/PCMDI/cmip6-cmor-tables/tree/master/Tables variable
name tables] are often applied to other climate data too, as there is
not yet a conventions around variable names.  
* CORDEX has similar [https://is-enes-data.github.io/cordex\_archive\_specifications.pdf
conventions] and [https://is-enes-data.github.io/CORDEX\_variables\_requirement\_table.pdf
variable tables ]

#### **Land ** 
* [https://www.lmd.jussieu.fr/\~polcher/ALMA/ ALMA data exchange
convention] the Assistance for Land-surface Modelling Activities group
estanblished conventions for land-surface schemes and their outputs.

#### **Ocean** 
* [https://arxiv.org/pdf/1911.08638.pdf
gridspec] defined by GFDL in 2019 as a standard for Earth System Model
grids to be included in the CF Conventions. It used for MOM5 and MOM6
grids. 
* [http://content.aodn.org.au/Documents/IMOS/Conventions/IMOS\_NetCDF\_Conventions.pdf
IMOS] has very specific extensions of the CF conventions for different
kind of ocean observation data, which has to be used if you want to
contribute data to their portal. 
* [http://www.oceansites.org/docs/oceansites\_data\_format\_reference\_manual.pdf
OceanSITES Data Format] - extension of CF Conventions standard for
OceanSITES data 
* [http://www.argodatamgt.org/Media/Medias-Argo-Data-Management/Argo-documentation/General-documentation/Data-format
ARGO netCDF conventions for data centers] 
* [https://www.pmel.noaa.gov/epic/document/convention.htm PMEL-EPIC
Conventions] 
* [https://www.ncei.noaa.gov/netcdf-templates US
NCEI NetCDF templates] - these templates illustrate how to apply CF and
ACDD conventions **Atmosphere** 
* [http://www.eol.ucar.edu/raf/Software/netCDF.html NCAR-RAF Conventions
for Aircraft Data] 

#### **Other** 
* [http://ambermd.org/netcdf/nctraj.xhtml AMBER Trajectory Conventions
for molecular dynamics simulations] 
* [http://cfconventions.org/Data/cf-conventions/cf-conventions-1.6/build/cf-conventions.html\#discrete-sampling-geometries
CF Discrete Sampling Geometries Conventions] - CF for observational and
point data 
* [http://ugrid-conventions.github.io/ugrid-conventions/
UGRID Conventions for unstructured (e.g. triangular, hex) grids.] 
* [http://sgrid.github.io/sgrid/ SGRID Conventions for staggered,
structured (e.g. ROMS, WRF) grids] 
* [https://www.unidata.ucar.edu/software/netcdf/conventions.html
UNIDATA NetCDF conventions lists] - including COARDS and other older
conventions
