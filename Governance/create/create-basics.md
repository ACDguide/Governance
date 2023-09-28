# Dataset creation basics

Climate data is a highly specialised field of data science, due to the size and complexity which often require computing and scientific coding skills. A variety of metadata fields are required to adequately describe the data and its dimensions. Domain-specific scientific knowledge is required to make informed decisions about its creation and use, and technical knowledge is required to produce robust datasets that can be reused by others. 
Many of the terms and concepts used are described in more detail in the [Concepts](../concepts/concept-intro.md) and [Technical tips](../tech/tech-intro.md) appendices.

## NetCDF format
By far the most commonly used format in the climate science community is [netCDF](../tech/data_formats.md): (maybe we should cross reference big data guide here)
* open,
* self-describing: metadata is an in-built feature,
* array-oriented,
 format.

NetCDF files contain three main components:

* Dimensions describe the overall array structure of the data stored in the file, though variables can have different dimensions. Dimensions can be ‘real’ dimensions (such as time, latitude, longitude), or ‘pseudo’ dimensions (such as land-use tiles, or spectral bands). NetCDF dimensions, however, contain no metadata or actual values, which are instead described using variables with the same name. The dimensions are the base architecture of the file.

```{note}
Technically, many dimensions can be created in a netCDF file, including multiple time or lat/lon dimensions.
However, it is recommended to minimise the use of multiple highly similar dimensions; particularly 'time', as often analysis/visualisation packages cannot handle multiple time axis and having more than one might produce errors or unexpected results. 
```

* Variables contain the actual value arrays and metadata used to describe them. NetCDF variables can be used for actual geospatial data (e.g., surface temperatures on a lat/lon grid), or to store the dimensions arrays and definitions (e.g., timestamps for a time dimension). Each variable is defined along one or more dimension and has associated attributes in the form of {key, value} pairs. Attributes and variable names must be strings, while there are only few restrictions on names, there are common standards (e.g., [CF conventions](../concepts/cf-conventions.md)) that we highly recommend using.


* Global attributes are {key: value} pairs that describe the overall file. These are typically chosen according to the kind of data, the way it was generated and its potential uses. However, standards such as the [ACDD conventions](../concepts/acdd-conventions.md) also exist to cover common global attributes. These include dataset title, [provenance information](../concepts/provenance.md), license, and contact information, as well as naming any metadata conventions implemented in the file.

```{note}
Raw scientific data is usually highly structured and likely in netCDF format already, so often the main effort required is to ensure that the attributes describe the data correctly and adequately. 
```

### Attributes

NetCDF metadata attributes are generally in one of two categories: machine-readable and human-readable (though these overlap significantly).

* Machine-readable attributes (e.g., `units`, `standard_name`, `missing_value` and `calendar`) typically describe the data itself, are usually variable-level, and can be automatically interpreted by standard plotting and analysis tools if set according to common [conventions](../concepts/conventions.md) and [controlled vocabularies](../concepts/controlled-vocab.md). These conventions typically contain suggestions for the attribute key and value using commonly understood terms and are highly recommended to enable analysis and visualisation with standard software packages. 

* Human-readable attributes (e.g., `title`, `institution`, `license` and `long_name`) are fields that contain free strings and are interpreted by the user. Often global-level, these tend to describe the larger context in which the dataset sits, and enable the user to understand where the data came from, how it was generated, and enables both reuse and reproduction. These attributes could document the climate model used to generate the data, the project in which the data generation was conducted, the contact information of the dataset creator or manager, or a list of [keywords](../tech/keywords.md) similar to those in a journal publication. 

CF conventions cover both variable-level and global attributes, while the ACDD conventions are an extension covering mostly 'human-readable' information.

````{note}
We give a detailed overview of how to write CF compliant files in the [Technical tips](../tech/conventions.md) appendix. This includes known issues that can be caused by not following the standards, as CF conventions are used by developers of tools that access and analyse netCDF data to make assumptions on the data structure. We recommend implementing these metadata fields in the post-processing workflow so that these are automatically generated when possible. For a more technical description of the netCDF format and metadata, see https://acdguide.github.io/BigData/data/data-netcdf.html.
````

:::{dropdown} Example of netCDF file with applied CF and ACDD conventions
netcdf DOLCE_v3_1980 {<br>
    dimensions:<br>
        lon = 1440 ;<br>
        lat = 720 ;<br>
        time = 12 ;<br>
    variables:<br>
        double lon(lon) ;<br>
            lon:units = "degrees_east" ;<br> 
            lon:long_name = "longitude" ;<br> 
            lon:standard_name = "longitude" ;<br> 
        double lat(lat) ;<br> 
            lat:units = "degrees_north" ;<br> 
            lat:long_name = "latitude" ;<br> 
            lat:standard_name = "latitude" ;<br> 
        double time(time) ;<br> 
            time:units = "days since 1970-1-1 0:0:0" ;<br> 
            time:long_name = "time" ;<br> 
            time:calendar = "gregorian" ;<br> 
            time:standard_name = "time" ;<br> 
        float hfls(time, lat, lon) ;<br> 
            hfls:units = "W m-2" ;<br> 
            hfls:_FillValue = NaNf ;<br> 
            hfls:long_name = "latent heat flux" ;<br> 
            hfls:standard_name = "surface_upward_latent_heat_flux" ;<br> 
            hfls:ALMA_short_name = "Qle" ;<br> 
        float hfls_sd(time, lat, lon) ;<br> 
            hfls_sd:units = "W m-2" ;<br> 
            hfls_sd:_FillValue = NaNf ;<br> 
            hfls_sd:long_name = "error (standard deviation) of latent heat flux" ;<br> 
            hfls_sd:standard_name = "surface_upward_latent_heat_flux" ;<br> 
            hfls_sd:cell_methods = "area: standard_deviation" ;<br> 

// global attributes:<br> 
    :title = "Derived Optimal Linear Combination Evapotranspiration (DOLCE) v3.0 " ;<br> 
    :history = "2021-03-29 22:57:39 v3.0" ;<br> 
    :institution = "University of New South Wales" ;<br> 
    :summary = "Hybrid Evapotranspiration dataset with error estimates" ;<br> 
    :product_version = "3.0" ;<br> 
    :creator_name = "Sanaa Hobeichi" ;<br> 
    :contact = "s.hobeichi@unsw.edu.au" ;<br> 
    :organisation = "ARC Centre of Excellence for Climate Extremes" ;<br> 
    :time_coverage_start = "1980-01-01" ;<br> 
    :time_coverage_end = "2018-12-31" ;<br> 
    :geospatial_lat_min = "-90" ;<br> 
    :geospatial_lat_max = "90" ;<br> 
    :geospatial_lon_min = "-180" ;<br> 
    :geospatial_lon_max = "180" ;<br> 
    :source = "ET from datasets: FLUXCOM MET, ERA5-land, GLEAM v3.5a, GLEAM v3.5b, and field observations from flux tower networks: FLUXNET2015, LaThuile Free Fair Use, CarboEurope, AmeriFlux, ARM, AsiaFlux, Oak Ridge, Ozflux" ;<br> 
    :id = "https://doi.org/10.25914/606e9120c5ebe" ;<br> 
    :keywords = "040105 Climatology (excl. Climate Change Processes) and 040608 Surfacewater Hydrology" ;<br> 
    :date_created = "2021-03-21" ;<br> 
    :Conventions = "CF-1.6, ACDD-1.3" ;<br> 
    :license = "http://creativecommons.org/licenses/by/4.0/" ;<br> 
    :references = "Hobeichi, S., Abramowitz, G., Evans, J. P. (2021): Derived Optimal Linear Combination Evapotranspiration v3.0 . NCI National Research Data Collection , doi:10.25914/606e9120c5ebe" ;<br> 
    :contributor_name = "CLEX data manager" ;<br> 
    :contributor_role = "curator" ;<br> 
    :contributor_email = "paola.petrelli@utas.edu.au" ;<br> 
:::

## File & directory organisation

Climate datasets are complex and can be chopped up and stored in many different ways. For example, datasets can broken up into separate files that contain full timeseries of a single variable, or each file could contain one month of data for all relevant variables. Data files should be structured into a navigable directory structure that sorts the files into some high-level dimensions that make it easier to access and understand what different data the set contains, with a directory tree that is meaningful and interpretable, and keeps the number of individual files in a given directory to below ~1000. Depending on how many files are produced, implementing a directory structure early before the number of files become hard to track, is recommended. Some suggestions for directory tree components/dimensions are: variable, frequency, modelling realm, experiment name, or governing project.

There is a type of complex directory structure known as a '[Directory Reference Syntax](../tech/drs.md)' (DRS), which is typically standardised through intercomparison projects such as CMIP and CORDEX. The directory tree components are usually very broad and cover many contextual aspects, especially when multiple models or modelling institutions are using the same directory structure and controlled vocabulary.

File naming is an important consideration here, as confusion can easily arise if you have not named your files with enough verbosity to disentangle similar, but critically different files. A common recommendation is to name the files in a similar way to the directory structure (e.g., if you have both monthly and daily data, put these into two separate sub-directories and include the frequency in the filenames). Other provenance details, such as experiment name and model, should be considered in the filename itself to reduce the risk of confusing different outputs. For example, a file called 'ocean_2014.nc' can be misunderstood very easily, but a file called 'ACCESS-ESM_historical-pacemaker_ocean_monthly_2014.nc' is much clearer and will reduce the risk of having to rerun models or misplacing irreplaceable observational data.  
See [this page](../tech/filenames.md) for some tips to creating a robust filenaming convention for your datasets.


## Backups & archiving

Climate data can often be difficult (or impossible) to regenerate, due to large compute costs and non-repeatable conditions. A good backup strategy is vital to ensuring that the risk of data loss is minimised, and storage/compute resources are used efficiently. It is also important to note that NCI's `/g/data` storage system is NOT backed up.

Our general recommendations are:
* keep only data intended for sharing in common areas.
* working data should be restricted to your personal space, or a defined collaborative working space.
* ancillary data (model input/config files, and other data that is not being actively used) tarred and archived into longer-term storage.
* raw data (e.g., unprocessed or semi-processed model output) should be backed up onto a tape system (e.g., NCI's [MDSS](../tech/massdata.md)) to enable regeneration of processed datasets from the raw data, without having to rerun models.
* a backup strategy should be set-up and implemented early (ideally as part of a data management plan; see next section).

For more detailed guidance on backing up data, see our [guide to creating a backup strategy](../concepts/backup.md) and [backup checklist](../tech/backup-checklist.md).

Moving data between disks (e.g., from NCI's `/scratch` to `/g/data/`) and systems (e.g., from NCI to public cloud) can be challenging, especially for datasets at the TB-scale. We recommend using [rsync](https://rsync.samba.org/) wherever possible, because it contains a large amount of flexibility (useful for the variety of use cases when moving data), and is generally very stable (stability is a major issue when moving data between systems). For more guidance on moving large data, see the [Moving Data page](../tech/moving-data.md).

## Data management plans & documentation

A **Data Management Plan** (DMP) is a general term for a document that describes the intended methods of the creation, storage, management and distribution of a given collection of data, and defines or cites the rules, policies or principles that govern the dataset. DMPs can vary greatly depending on context, the type of data, or intended audience. A DMP is also a living document, one that evolves through the various stages of the project in which the data is created.  
Generally, however, a DMP should provide guidance to data managers to inform decision making. E.g., where should a new dataset be stored, who should have access to it, when should it be deleted. In the case where decisions are not clearly indicated from the DMP, it should indicate who is responsible for making the decision.  
Ideally, a DMP is prepared as an integral part of project planning, with a data custodian also responsible for its continued development. An initial DMP can be as simple as notes in a text file, and include basic information such as backup locations, input files, tools used, and the intended use of the final dataset. Additionally, file metadata such as licences (see https://acdguide.github.io/Governance/concepts/license.html) and contact information are regularly included in DMPs. 

For more information on Data Management Plans, see https://acdguide.github.io/Governance/concepts/dmp.html

While similar to a DMP in many ways, **data documentation** is a distinct purpose in that it provides guidance to users of the data (rather than managers of the data), including those who intend to reproduce it. Data documentation will include many of the same information as a DMP, such as the method of data generation (input files, software used), distribution details, and project context. Data documentation is typically kept alongside the dataset as in a README file at the top level directory, which provide high-level information about the dataset (e.g., when it was created, who to contact, and how to use it). However, data documentation is a general term for 'user guidance of a dataset' and can also be prepared in the form of journal articles that provide much more detail. In cases where the data itself is not self-describing (e.g., CSV files), data documentation will need to provide low-level metadata such as dimensions and units.

(possibly too much info for data creartion scope)



## Code management & version control

Claire:  
If your data is an analysis product, keep the code nearby the data or document where it can be accessed (snapshot the version of the code used to create this dataset)

Paola:  
Keep code under version control

Chloe:  
Versioning: https://acdguide.github.io/Governance/tech/versioning.html
