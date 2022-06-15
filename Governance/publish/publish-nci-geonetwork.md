# Publishing climate data with NCI

NCI provides web services to publish data and metadata:
* a [dataset catalogue](https://geonetwork.nci.org.au/geonetwork/srv/eng/catalog.search#/home) based on [GeoNetwork](geonetwork) to describe the dataset (i.e. a metadata repository) and associated DOI.  This will be the landing page for the DOI and will include a link to access the dataset. 
* a [THREDDS Data Server](https://dapds00.nci.org.au/thredds/catalog.html) (TDS) this is a public data repository that provides access to the data. [THREDDS](thredds) offer a variety of protocols, files can be downloaded from here or accessed via the [OPeNDAP protocol](opendap).

## What data can be published with NCI
Publishing with NCI is a good option when publishing a big dataset and/or data in NetCDF format. Obvious candidates are outputs of model simulation run on Gadi. 
THREDDS was developed for NetCDF files, publishing on a THREDDS server means that data is also available by OPeNDAP. This is useful when publishing a big dataset or the data is stored in big files. OPeNDAP allows remote access, a user can subset the data which avoids downloading the entire dataset. OPeNDAP protocol can be used with several analysis software. 

## Generic procedure to publish with NCI
Currently NCI is in the process of updating their data procedures, their [official documentation](https://opus.nci.org.au/display/NDP/NCI+Data+Collections+and+Publishing) does not yet include a detailed description of the process, so the following information is based on our experiences.

### Data project
NCI manages storage and computational resources via projects. To publish data with them a project setup exclusively for this scope is needed. Depending on the researcher's affiliation and or the dataset scope, they might be able to contribute to an existing "publishing" data project. This is a good option if the dataset is relatively small, as NCI is unlikely to setup a project for a small dataset. An example is the CLEX collection which uses project ks32.

If the dataset is big enough to have its own project, then the researcher should contact the NCI data team, via the helpdesk, and discuss their options with them. If NCI agrees, the researcher will have to provide details of the dataset and usually funding for the disk storage.

### Creating a geonetwork record
The first step is to create a DMP to collect information on the dataset. Currently NCI uses google spreadsheet to do so. Once NCI has agreed to publish the dataset, they will create a spreadsheet to fill. An example from the publication of a satellite dataset is available [here](https://docs.google.com/spreadsheets/d/1Rt-bKNfjNRi-kB_pFrhLE9-XwqvmkpLfu5i4_sdzfQ4/edit#gid=0).   
Once the form is ready NCI will use the content to create a geonetwork record and mint a DOI for the new dataset. The geonetwork record will provide the landing page for the DOI and will be visible only once the files are available on THREDDS.

### Preparing the files
The actual files have to be organised in a <dataset-folder>, this will contain the license and a readme files (usually pointing to the geonetwork record) and a sub-folder for each version containing the data files. How the data is organised will depend on the actual dataset, see the [DRS page](../tech/drs.md) for examples.
The files should follow both [CF](../concepts/cf-conventions.md) and [ACDD](../concepts/acdd-conventions.md) conventions. Once the files are ready NCI will run a QC check, as well as checking for CF/ACDD compliance, they will check that the files are accessible by widely used software like ncview, nco etc.
If the files passed the tests, then they will the dataset to THREDDS and activate the DOI. If not, they will send a detailed report of the QC results so the files can be fixed where possible.
CLEX CMS team has installed the IOOS CF-checker NCI uses and created a simple python wrapper that create a similar report to the NCI's one. These can be used to check the files before submitting them to NCI. Details are on the [CLEX CMS wiki](http://climate-cms.wikis.unsw.edu.au/CF_checker).

## Existing data collections

### CLEX
CLEX has its own data collection in project ks32, anyone associated with CLEX can publish a dataset in this collection.
The [CLEX CMS wiki](http://climate-cms.wikis.unsw.edu.au/Publishing_with_NCI) has plenty of information on the process. CLEX currently manages a DMP web tool, so they use that to collect information on the dataset. The relevant parts of the DMP are then used to generate a geonetwork xml file that can be directly uploaded by NCI, instead of filling the spreadsheet form.
However, this might change in the future as NCI is trying to have a reference page on confluence for each dataset. 

### CSIRO

### BoM
