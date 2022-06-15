# Publishing climate data with NCI

NCI provides web services to publish data and metadata:
* a [dataset catalogue](https://geonetwork.nci.org.au/geonetwork/srv/eng/catalog.search#/home) based on [GeoNetwork](geonetwork) to describe your dataset (i.e. a metadata repository) and associated DOI.  This will be the landing page for the DOI and will include a link to access the dataset. 
* a [THREDDS Data Server](https://dapds00.nci.org.au/thredds/catalog.html) (TDS) this is a public data repository that provides access to the data. [THREDDS](thredds) offer a variety of protocols, files can be downloaded from here or accessed via the [OPeNDAP protocol](opendap).

## What data can you publish with NCI
Publishing with NCI is a good option when you want to publish a big dataset and/or data in NetCDF format. Obvious candidates are outputs of model simulation run on Gadi. 
The THREDDS was developed for and it is well suited to NetCDF files, publishing on a THREDDS server means that your data can also be avaialble by OPeNDAP. This is really useful if you are publishing a big dataset or the data is stored in big files. OPeNDAP allows remote access, a user can subset the data which avoids downloading the entire dataset. OPeNDAP protocol can be used with several analysis softwares. 

## Data project
NCI manages storage and computational resources via projects. To publish your datas with them you need a project setup exclusively for this scope. Depending on who you are affiliated with you might have access to an existing "publishing" data project you can contribute to. This is a good option if your dataset is relatively small, as NCI is unlikely to setup a project for a small dataset. An example is the CLEX collection which uses project ks32.

If your dataset is big enough to have its own project then you can contact the NCI data team, you can create a helpdesk ticket to do so, and discuss your options with them. If NCI agrees you will have to provide details of the dataset and usually funding for the disk storage.

## generic procedure to publish with NCI
Currently NCI is in the process of updating some of their data procedures, there is no official documentation on how to publish data with them, the following information is based on our experiences.

### Creating a geonetwork record
The first step is to create a DMP to collect information on the dataset. Currently NCI uses their confluence website to do so. Once you contacted them and agreed to publish with them, they will create a confluence page for you to access with a form to fill.  (put template in separate page).   
Once the form is ready NCI will use the content to create a geonetwork record and mint a DOI for the new dataset. The geonetwork record will provide the landing page for the DOI and will be visible only once the files are available on THREDDS.

### Preparing the files
The actual files has to be organised in a <dataset-folder> with a license.txt and readme.txt file plus sub-folders for the actual files. How the data is organised will depend on the actual dataset, see DRS page. The readme.txt file will only contain a reference to the geonetwork record.
The files should follow both [CF](cf-conventions) and [ACDD](ACDD-conventions) conventions. Once the files are ready NCI will run a QC check, as well as checking for CF/ACDD compliance, they will check that the files are accessible by widely used software like ncview, nco etc.
If the files passed the tests then they will the dataset to THREDDS and activate the DOI. If not they will send a detailed report of the QC results so you can fix the files where possible.
CLEX CMS team has installed the IOOS CF-checker NCI uses and created a simple python wrapper that create a similar report to NCI. You can use these to check your files before submitting them to NCI. Details are on the [CLEX CMS wiki](http://climate-cms.wikis.unsw.edu.au/CF_checker).

## Existing data collections

### CLEX
CLEX has its own data collection in project ks32, anyone associated with CLEX can publish a dataset in this collection.
The CLEX CMS wiki has plenty of information on the process. CLEX currently manages a DMP web tool, so they use that to collect information on the dataset. The relevant parts of the DMP are then used to generate directly a geonetwork xml file that can be directly uploade by NCI.
In this way there is no need to fill ina the form in confluence. However, this might change in the future as NCI is trying to have a reference page on confluence for each dataset. 

### CSIRO

### BoM
