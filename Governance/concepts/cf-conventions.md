# CF Conventions
The [CF conventions](https://cfconventions.org) are specifically designed to facilitate the processing and sharing of netCDF files. They are based on the older [COARDS conventions](https://ferret.pmel.noaa.gov/noaa\_coop/coop\_cdf\_profile.html), which they extend. The first version (v1.0) of the CF Conventions was released in 2003, the current version (in 2021) is v1.8. Each new version tries, as much as possible, to be compatible with older versions. The first versions, as the name implied were focusing on climate and forecast data, since then they broaden their scope to earth
data in general, including observational data.
CF is now widely adopted as the main standard both in the production of netCDF related code and for the publication of netCDF data. As the initial focus was to allow interoperability of netCDF based software packages, the conventions main aim is to define clearly each variable and the spatial and temporal properties of the data. Applying these Conventions to your netCDF files makes them more re-usable.
Most software used in Climate science will know how to open and process correctly the files. The metadata required will describe clearly the characteristic of the data in the files, making it easier to identify correctly the variables and compare them to similar data. CF Conventions focus mostly on the variable and dimensions description, the full Conventions document is quite long but, in most cases, you will be using the same attributes. This [CMS Blog](https://climate-cms.org/2018/10/26/Setting-up-NetCDF-file-attributes.html) provides an example on how to apply them to your data, covering the attributes most commonly required.

Important elements of the Conventions are: 
* the [UDUNITS2](https://ncics.org/portfolio/other-resources/udunits2/?)
packages for units' standards 
* the [standard_name](https://cfconventions.org/Data/cf-standard-names/77/build/cf-standard-name-table.html) whose scope is to provide a common terminology for variables names. For example, every variable with the standard_name **air_temperature** can be defined as 
>"Air temperature is the bulk temperature of the air, not the surface (skin) temperature."
> with K or equivalent units, regardless of the way the actual variable is
named in the file. 
```{warning}
Standard_name is a very useful attribute but should be applied with attention. It is better to leave it out if a suitable one is not available.
```
There are various tools available to help you check your files against a version of the CF Conventions. The CLEX CMS covered some on their [wiki](http://climate-cms.wikis.unsw.edu.au/CF_checker).    
