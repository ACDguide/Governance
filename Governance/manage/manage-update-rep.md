# Updates to replicated data
Updates to replicated data can be regular or run upon request. 

## Regular updates

This should be executed by the same code used to perform the first bulk download. Some datasets are updated regularly and you can set up a similarly frequent automatic update to keep up with the original data updates schedule.
If updates are irregular some data providers will notify registered users of new versions or error in the data. It is a good idea tosubscribe to any such service even if it is not a requirement. The dataset documentation shpuld also share these services and how to subscribe, encouraging users of the dataset to also received updates and news around the data. This also helps data provider to have a more relaistic idea of how many people are using their data.
In other case the updates are needed only sporadically when issues are found with the current dataset or a new version is released. Not all data providers notify users of these changes, indeed it's unfortunately not rare for files to be changed with no announcement at all.
If you know the data is likely to be updated but you have no idea of the frequency still set a reasonable interval (as monthly) to check for updates.
If a data provider is prone to change data without warnings then you should make sure to have a really robust system to check for changes in the files themselves, ie.e checksum or last modified date.
NB a form of warning could be in the filenames themselves, some data provider include a creation date in the filename.

## Data downloaded or updated on request

When replicating data from big data collection as CMIP6 or ERA5 it is usual to download only subsets that local users need, rather than the entire collection which would be too big to host. With this use case is important to have a system to handle the requests and to check for specific updates of the subset already downloaded. The best way to do so is to have a database with an associated code that can create, update and query the database itself.

Example of this approach are the [CleF](https://zenodo.org/record/4729030#.Ytdh6C8RqRs) which was built to manage ESGF data, this [ERA5 code](https://zenodo.org/record/3972437#.Ytdhky8RqRs) which was used to manage the first ERA5 collection at NCI, [cosima-cookbook](https://github.com/COSIMA/cosima-cookbook#readme) which as well as listing the cosima model output aslo offers a suite of functions to analyse the data.
 
