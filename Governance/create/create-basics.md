# Dataset creation basics & sharing recommendations

See https://github.com/ACDguide/Governance/issues/7 for discussion and suggestions 


## File formats, metadata & coordinates

Climate data is a highly specialised field of data science, due to the size and complexity which often require computing and scientific coding skills, the variety of metadata fields required to adequately describe the data and its dimensions, the domain-specific scientific knowledge required to make informed decisions about its creation and use, and the technical knoweldge required to produce robust datasets that can be reused by others. (Note that we will use terms and concepts described in the appendix [Concepts](../concepts/concept-intro.md).)

By far the most commonly used format in the climate science community is [netCDF](https://www.unidata.ucar.edu/software/netcdf/), an open (i.e. not proprietary), self-describing (i.e. metadata is an in-built feature) array-oriented (i.e. highly structured data such as climate model data) format that is typically used on POSIX systems (Unix-based computing system with a directory structure and command-line input; standard for high-performance computing systems such as [NCI](https://nci.org.au/)). See the [technical note on data formats](../tech/data_formats.md).

### Components of a NetCDF file

NetCDF files contain three main components:

* Dimensions describe the overall array structure of the data stored in the file, though not every variable must use all dimensions that exist in the file. Dimensions can be ‘real’ dimensions (such as time, latitude, longitude), or ‘pseudo’ dimensions (such as land-use tiles, or spectral bands). NetCDF dimensions, however, contain no metadata or actual values, which are described using variables with the same name. The dimensions are the base architecture of the file.

```{note}
Technically, many dimensions can be created in a NetCDF file, including multiple time (e.g. time0, time 1, etc) or lat/lon (e.g. lat_a, lat_c) dimensions if you choose.
However, it is recommended to minimise the use of multiple highly similar dimensions; particularly 'time', as there is often a hard-coded expectation in analysis/visualisation packages that expect one and only one time axis.  
```

* Variables (usually represented with floating point values) contain the actual geospatial data that you are interested in storing and sharing. NetCDF variables can be either your specific scientific information (e.g. surface temperatures on a lat/lon grid), or the value description of the array dimensions (e.g. timestamps for a time dimension). Each variable is defined along one or more dimension, and has associated attributes in the form of key:value pairs. These attributes can be titled using any string or value, however there are some common standards (e.g. [CF conventions](../concepts/cf-conventions.md)) that we highly recommend using.

* Global attributes are key:value pairs that descibe the file at the top-level. While these are typically chosen according to the use case of the data and can vary significantly between modelling realms or scientific need, standards also exist for these. Common global attributes include dataset title, provenance information (i.e. where the data came from), license, and contact information, as well as naming any metadata conventions implemented in the file.

It is likely that the raw scientific data that you are building your datasets around are already highly structured (even in netCDF format already), so your main effort here will be ensuring that the metadata correctly and adequately describes your data. 

### Attributes

NetCDF metadata attributes are generally in one of two categories: machine-readable and human-readable (though these overlap significantly).

* Machine-readable attributes (e.g., `units`, `standard_name`, `missing_value` and `calendar`) typically describe the data itself, are usually variable-level, and can be automatically interpreted by standard plotting and analysis tools if set according to common [conventions](../concepts/conventions.md) and [controlled vocabularies](../concepts/controlled-vocab.md). These conventions typically contain suggestions for the attribute key and value using commonly understood terms, and are highly recommended to enable analysis and visualisation with standard software packages. 

* Human-readable attributes (e.g. `title`, `institution`, `license` and `long_name`) are fields that contain free strings and are interpreted by the user. Often global-level, these tend to describe the larger context in which the dataset sits, and enable the user to understand where the data came from, how it was generated, and enables both reuse and reproduction. These attributes could document the climate model used to generate the data, the project in which the data generation was conducted, the contact information of the dataset creator or manager, or a list of [keywords](../tech/keywords.md) similar to those in a journal publication. Conventions usually contain suggested keys to use, with the values defined according to your use case.

For a list of recommended attributes to include and define in most climate datasets and how to apply them, see the [conventions page in this book](../tech/conventions.md). We recommend implementing these metadata fields into your post-processing workflow so that these are automatically applied by your data creation code/script. 

For a more technical description of the netCDF format and metadata, see https://acdguide.github.io/BigData/data/data-netcdf.html.

### Example metadata using ncdump

Ncdump from a simple-ish file. Not CMIP6, coz I want to save that for later; prefer something less complex.

## File & directory organisation

Climate datasets are complex and can be chopped up and stored in many different ways. For example, datasets can broken up into separate files that contain full timeseries of a single variable, or each file could contain one month of data for all relevant variables. Data files should be structured into a navigable directory structure that sorts the files into some high-level dimensions that make it easier to access and understand what different data the set contains, with a directory tree that is meaningful and interpretable, and keeps the number of individual files in a given directory to below ~1000. Depending on how many files are produced, implementing a directory structure early before the number of files become hard to track, is recommended. Some suggestions for directory tree components/dimensions are: variable, frequency, modelling realm, experiment name, or governing project.

There is a type of complex directory structure known as a '[Directory Reference Syntax](../tech/drs.md)' (DRS), which is typically standardised through intercomparison projects such as CMIP and CORDEX. The directory tree components are usually very broad and cover many contextual aspects, especially when multiple models or modelling institutions are using the same directory structure and controlled vocabulary.

Filenaming is an important consideration here, as confusion can easily arise if you have not named your files with enough verbosity to disentangle similar, but critically different files. A common recommendation is to name the files in a similar way to the directory structure (e.g. if you have both monthly and daily data, put these into two separate sub-directories and include the frequency in the filenames). Other provenance details, such as experiment name and model, should be considered in the filename itself to reduce the risk of confusing different outputs. For example, a file called 'ocean_2014.nc' can be misunderstood very easily, but a file called 'ACCESS-ESM_historical-pacemaker_ocean_monthly_2014.nc' is much clearer and will reduce the risk of having to rerun models, or misplacing irreplaceable observational data.  
See [this page](../tech/filenames.md) for some tips to creating a robust filenaming convention for your datasets.


## Backups & archiving

Climate data can often be difficult (or impossible) to regenerate, due to large compute costs and non-repeatable conditions. A good backup strategy is vital to ensuring that the risk of data loss is minimised, and storage/compute resources are used efficiently. It is also important to note that NCI's `/g/data` storage system is NOT backed up.

Our general recommendations are:
* keep only data intended for sharing in common areas.
* working data should be restricted to your personal space, or a defined collaborative working space.
* ancillary data (model input/config files, and other data that is not being actively used) tarred and archived into longer-term storage.
* raw data (e.g. unprocessed or semi-processed model output) should be backed up onto a tape system (e.g. NCI's [MDSS](../tech/massdata.md)) to enable regeneration of processed datasets from the raw data, without having to rerun models.
* a backup strategy should be set-up and implented early (ideally as part of a data management plan; see next section).

For more detailed guidance on backing up data, see our [guide to creating a backup strategy](../concepts/backup.md) and [backup checklist](../tech/backup-checklist.md).

Moving data between disks (e.g. from NCI's `/scratch` to `/g/data/`) and systems (e.g. from NCI to public cloud) can be challenging, especially for datasets at the TB-scale. We recommend using [rsync](https://rsync.samba.org/) wherever possible, because it contains a large amount of flexibility (useful for the variety of use cases when moving data), and is generally very stable (stability is a major issue when moving data between systems). For more guidance on moving large data, see the [Moving Data page](../tech/moving-data.md).

## Data management plans & documentation

A **Data Management Plan** (DMP) is a general term for a document that describes the intended methods of the creation, storage, management and distribution of a given collection of data, and defines or cites the rules, policies or principles that govern the dataset. DMPs can vary greatly depending on context, the type of data, or intended audience. A DMP is also a living document, one that evolves through the various stages of the project in which the data is created.  
Generally, however, a DMP should provide guidance to data managers, in order to help inform decision making. E.g., where should a new dataset be stored, who should have access to it, when should it be deleted. In the case where decisions are not clearly indicated from the DMP, it should indicate who is responsible for making the decision.  
Ideally, a DMP is prepared as an integral part of project planning, with a data custodian also responsible for it's continued development. An initial DMP can be as simple as notes in a text file, and include basic information such as backup locations, input files, tools used, and the intended use of the final dataset. Additionally, file metadata such as licences (see https://acdguide.github.io/Governance/concepts/license.html) and contact information are regularly included in DMPs. 

For more information on Data Management Plans, see https://acdguide.github.io/Governance/concepts/dmp.html

While similar to DMP in many ways, **data documentation** is a distinct purpose in that it provides guidance to users of the data (rather than managers of the data), including those who intend to reproduce it. Data documentation will include many of the same information as a DMP, such as the method of data generation (input files, software used), distribution details, and project context. Data documentation are typically kept alongside the dataset as in a README file at the top level directory, which provide high-level information about the dataset (e.g., when it was created, who to contact, and how to use it). However, data documentation is a general term for 'user guidance of a dataset', and can also be prepared in the form of journal articles that provide much more detail. In cases where the data itself is not self-describing (e.g. CSV files), data documentation will need to provide low-level metadata such as dimensions and units.



## Code management & version control

Best practice for managing software of any kind starts with *version controlled repositories*. Git-based platforms (e.g., GitHub and GitLab instances such as the [NCI GitLab](https://git.nci.org.au/)) and APIs are the current standard, although SVN and other tools are also in use throughout climate science. Learning these tools are vital to software development, and the versioning native in these systems help ensure provenance, reproduction, and creating FAIR datasets for sharing and publication. 
Releases (Git-based publications) of specific versions can be useful to complement published datasets or papers, however it is important to note that independent publication of code (e.g. via Zenodo) is required for a DOI and is recommended to ensure long-term access and reproducibility.

Of course, code cannot exclusively exist in a repository. It is suggested (particularly if your data is an analysis product) to keep the code nearby the data (e.g. in the same parent directory) or document where it can be accessed in a readily available README file (also note the version of the code used to create the associated dataset!). 

Data should also be versioned, especially for more underpinning datasets such as model output & data products, however best practice in this domain is still evolving. CMIP data includes versioning at the variable level that uses date of file creation, however this is just one method. 

For more information on versioning, see https://acdguide.github.io/Governance/tech/versioning.html
