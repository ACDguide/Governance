# Updates to replicated data
Updates to replicated data can be regular or run upon request. 

## Regular updates

This should be executed by the same code used to perform the first bulk download. Some datasets are updated regularly, and similarly frequent automatic updates should be set up to keep up with the original data updates schedule.
If updates are irregular some data providers will notify registered users of new versions or errors in the data. It is a good idea to subscribe to any such service even if it is not a requirement. The dataset documentation should also share these services and how to subscribe, encouraging users of the dataset to also receive updates and news around the data. This also helps the data provider to have a more realistic idea of how many people are using their data.
Sometimes updates are needed only sporadically when issues are found with the dataset, or a new version is released. Not all data providers notify users of these changes, indeed it is unfortunately not rare for files to be changed with no announcement at all.

Setting a reasonable interval, based on the previous updates history to check for updates, is a good startegy to avoid missing unexpected changes to the original data, but at the same time avoiding running updates too often.
If a data provider is prone to change data without warnings, then it is important to ensure a really robust system is in place to check for changes in the files themselves, i.e. checksums or last modified date.

```{note}
NB a form of warning could be in the filenames themselves, some data providers include a creation date in the filename.
```

## Data downloaded or updated on request

When replicating data from a big data collection such as CMIP6 or ERA5, it is usual to download only subsets that local users need, rather than the entire collection which would be too big to host. With this use case, it is important to have a system to handle the requests and to check for specific updates of the subset already downloaded. For datasets distributed by the ESGF, it is possible to use the python module [synda](https://prodiguer.github.io/synda/). Synda is what NCI is using to manage the CMIP5 and CMIP6 collections and it is an example of a database with an associated code that can create, update, and query the database itself. A user can put a request via a google form, their helpdesk or CleF (see below) as described on their [confluence CMIP space](https://opus.nci.org.au/display/CMIP/Data+Download+Request). 

Other examples of this approach are:
*  [CleF](https://zenodo.org/record/4729030#.Ytdh6C8RqRs) which was built to allow NCI users to query ESGF data; 
* this [ERA5 code](https://zenodo.org/record/3972437#.Ytdhky8RqRs) which was used to manage downloads for the temporary ERA5 collection at NCI;
* a modification of the same to download CMIP6_ETCCDI climate indices;
* the [cosima-cookbook](https://github.com/COSIMA/cosima-cookbook#readme) which as well as listing the cosima model output also offers a suite of functions to analyse the data.
 
