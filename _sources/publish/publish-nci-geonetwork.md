# Publishing climate data with NCI

NCI provides web services to publish data and metadata:
* a [dataset catalogue](https://geonetwork.nci.org.au/geonetwork/srv/eng/catalog.search#/home) based on [GeoNetwork](geonetwork) to describe the dataset (i.e. a metadata repository) and associated DOI.  This will be the landing page for the DOI and will include a link to access the dataset. 
* a [THREDDS Data Server](https://dapds00.nci.org.au/thredds/catalog.html) (TDS). This is a public data repository that provides access to the data. [THREDDS](thredds) offer a variety of protocols, and files can be downloaded from here or accessed via the [OPeNDAP protocol](opendap).

## What data can be published with NCI
Publishing with NCI is a good option when publishing a big dataset and/or data in netCDF format, with obvious candidates being outputs of model simulation runs on Gadi. 
THREDDS was developed for netCDF files, and publishing on a THREDDS server means that data is also available by OPeNDAP, which can be used with several analysis software packages. This is useful when publishing a big dataset or the data is stored in big files, since OPeNDAP allows remote access where a user can subset the data and avoid downloading the entire dataset. 

## Generic procedure to publish with NCI
Currently NCI is in the process of updating their data procedures, their [official documentation](https://opus.nci.org.au/display/NDP/Data+Management) does not yet include a detailed description of the process, so the following information is based on our experiences.

### Data project
NCI manages storage and computational resources via projects. To publish data with them a project setup exclusively for this scope is needed. Depending on the researcher's affiliation and or the dataset scope, they might be able to contribute to an existing "publishing" data project. This is a good option if the dataset is relatively small, as NCI is unlikely to setup a project for a small dataset. An example is the CLEX collection which uses project ks32.

If the dataset is big enough to have its own project, then the researcher should contact the NCI data team, via the helpdesk, and discuss the options with them. If NCI agrees to proceed with the publication, the researcher will have to provide details of the dataset and usually funding for the disk storage.

### Creating a GeoNetwork record
The first step is to create a DMP to collect information on the dataset. Once NCI has agreed to publish the dataset, they will create a page on their confluence site for the specified project, containing a table to be populated with the dataset information.
These pages are only visible to interested parties, therefore we provide an [example](https://docs.google.com/spreadsheets/d/1Rt-bKNfjNRi-kB_pFrhLE9-XwqvmkpLfu5i4_sdzfQ4/edit#gid=0) from the publication of a satellite dataset, using a google spreadsheet instead.
Once the DMP is ready NCI will use the content to create a geonetwork record and mint a DOI for the new dataset. The GeoNetwork record will provide the landing page for the DOI and will be visible only once the files are available on THREDDS.

### Preparing the files
The actual files have to be organised in a <dataset-folder>, this will contain the license and a readme file (usually pointing to the geonetwork record) and a sub-folder for each version containing the data files. How the data is organised will depend on the actual dataset, see the [DRS page](../tech/drs.md) for examples.
The files should follow both [CF](../concepts/cf-conventions.md) and [ACDD](../concepts/acdd-conventions.md) conventions. Once the files are ready, NCI will run a QC check, CF/ACDD compliance check, and that the files are accessible by widely used software like ncview, nco etc.
If the files passed the tests, then they will add the dataset to THREDDS and activate the DOI. If not, they will send a detailed report of the QC results so the files can be fixed where possible.

```{admonition} CF-checker
CLEX CMS team has installed the IOOS CF-checker NCI uses and created a simple python wrapper that creates a similar report to the NCI one. These can be used to check the files before submitting them to NCI. Details are on the [CLEX CMS wiki](http://climate-cms.wikis.unsw.edu.au/CF_checker).
```

## Existing data collections

### CLEX
CLEX has its own data collection in project [ks32](https://my.nci.org.au/mancini/project/ks32), anyone associated with CLEX can publish a dataset in this collection.  
The [CLEX CMS wiki](http://climate-cms.wikis.unsw.edu.au/Publishing_with_NCI) has plenty of information on the process. CLEX currently manages a DMP web tool, which they use to collect information on the dataset. The relevant parts of the DMP are then used to generate a geonetwork xml file that can be directly uploaded by NCI, instead of populating the DMP on a confluence page.

### CSIRO
The Australian contribution to CMIP6 is published in project [fs38](https://my.nci.org.au/mancini/project/fs38), and to CMIP5 in project [rr3](https://my.nci.org.au/mancini/project/rr3)

### BoM
The [Australian Water Outlook Service Data Collection](https://my.nci.org.au/mancini/project/iu04) is published in project iu04.  
The [Australian Gridded Climate Data (AGCD) Collection](https://my.nci.org.au/mancini/project/zv2) is published in project zv2.

### NCI
[Reference Datasets for Climate Model Analysis/Forcing](https://my.nci.org.au/mancini/project/qv56), in project qv56 which includes Obs4MIPs and input4MIPs.  
The MERRA2 6-hourly reanalysis data is stored in project [rr7](https://my.nci.org.au/mancini/project/rr7)
