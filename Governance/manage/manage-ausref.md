# Australian Community Reference Climate Data Collection @ NCI

This collection is a collaboration between the Australian Climate Service (ACS), ARC Centre of Excellence for Climate Extremes (CLEX) and the wider Australian climate research community to re-establish and maintain a reference dataset collection at NCI.
We chose this collection as a use case as we are directly involved in managing this collection. But most importantly because one of the aims of this collection is to provide the climate community with well-documented, easy to discover and easy to access datasets. The collection was launched in July 2022 and is still growing.

## Code management

The codes used to download and update the data are shared and documented using GitHub.  

## NCI project 
This collection is hosted in the `ia39` data project, this project also hosts other related climate datasets.
Anyone can request access to the project, while a select group of managers are also part of the `ia39_w` writers' group.
The writers group uses ACLs to make sure anyone in `ia39` has access to the data but only the data managers can update, add and/or delete files.

## Directory structure
The main collection directory is

```{code}
/g/data/ia39/aus-ref-clim-data-nci/
```
Each dataset has a lowercase acronym used to label their main folder, with two sub-folders; one for `code` and one for `data`

```{code}
/g/data/ia39/aus-ref-clim-data-nci/cmorph/code
/g/data/ia39/aus-ref-clim-data-nci/cmorph/data
```

The `code` directory is a clone of the related GitHub repository, so it contains the code and the log updates, and is kept under version control. Wherever possible the same structure and names are used, for example, all the logs are called `updates_log.txt`. 

## Regular updates
On the NCI server only system administrators can run cronjob, to get around this limitation, regular dataset updates are managed using a [Jenkins server](https://accessdev.nci.org.au/jenkins/job/aus-ref-clim-data-nci/). A workflow is run at regular intervals for each dataset, the workflow settings, status, and logs are publicly visible. Where Jenkins is used to update a dataset, details are also documented in the dataset `README` file.

## Documentation

As mentioned above, each dataset has its own associated GitHub repository. This is the main documentation at dataset level. The same template is used for all the `README.md` files to make sure that all the important elements (such as DOIs, license, references, sources etc.) are covered. [See here](https://aus-ref-clim-data-nci.github.io/aus-ref-clim-data-nci/collection/howto.html#add-a-new-dataset) for details. 
The main documentation at collection level is provided via a [Jupyter book](https://aus-ref-clim-data-nci.github.io/aus-ref-clim-data-nci/intro.html). Jupyter books are managed entirely as a GitHub repository, so they are well set for collaboration and for end-users to add comments and/or requests by creating an issue, if necessary.
The Jupyter Book contains detailed information on the collection scope, governance, and management, including how other community members can contribute.
The `README.md` files of each dataset repository are used to create a list of the dataset's documentation.
With this approach no matter how a user accessed this information, via GitHub, locally or through the Jupyter Book it will always be synchronised.

## Listing on online data portal

The datasets included in the collection are all replicas, as such publishing a record on a climate related repository or on the NCI geonetwork catalogue it is not an option. However, each dataset will be listed in a new [Australian Climate Data Guide catalogue](https://oneclimate.dmponline.cloud.edu.au/records/xj8jz-7qq73). This is also a community project and accepts any Australian climate related resource. The portal cannot mint new DOIs but can list both published datasets with an existing DOI and replicated datasets. A record will be created for each dataset (or more than one where dataset had different versions available), each record shows the documentation, where to find the data at NCI, has links to the original official documentation and lists, where available, the original DOIs.

## Intake catalogue 
Many people working in climate science and other related earth science disciplines use python to perform analysis on data. For this reason, a lot of python climate related modules exist. One example is [Intake](https://intake.readthedocs.io/en/latest/), this package is used to build data catalogues, which are Pandas dataframes. Intake allows a user, for example, to query, subset, and access netCDF data directly as Xarray datasets. This collection uses an [Intake catalogue](https://github.com/aus-ref-clim-data-nci/acs-replica-intake) to list all the available datasets. The Intake catalogue is updated regularly, with updates managed by the Jenkins server as for the dataset updates. The catalogue is also installed in the CMS python conda environments so it can be loaded more easily. A [jupyter demo notebook](https://github.com/aus-ref-clim-data-nci/acs-replica-intake/blob/main/acs-replica-demo.ipynb) shows how to use the catalogue.
