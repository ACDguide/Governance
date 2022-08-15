# File handling

This part covers how to manage the actual files and directories, starting from the download process, and applies mostly to replicated datasets. A description of how to name and organise the files of a new dataset is covered in the section [Creating dataset guidelines](../create/create-intro.md). 

## Managing downloads

How to manage downloads depends mostly on how the original data is distributed and on how big the dataset is. Often servers offer more than one option to download the data. 
It is good practice to always create a dedicated code, as this is also a way to document exactly where the data was downloaded from and how. 
Even if a dataset is composed of one or few files that could easily be downloaded from a web interface and regular updates are not needed.
Bash scripts are fine if the downloads are quite simple; in the above example we can retrieve files with a simple `wget` or `curl`. If there is a lot of shuffling of files and directories to do, a bash script can become quickly complicated and unreadable, in these cases a proper coding language should be sued. 
Python is a good choice for a scripting language as it has lots of modules that can help with downloads, for example:
   * ftplib - to handle FTP servers
   * requests - to handle HTTP, FTP requests including authentication
   * BeautifulSoup - to scrape webpages
   * os and sys - to interact with the file system
   * logging - to create logs with different levels of severity 
   * data structure like dictionaries that help mapping terms

A good code should be:
  * efficient
  * flexible enough to adapt easily to different versions or subsets of the same data
  * log a list of files that were downloaded, updated or that presented errors
  * if authentication is needed, passwords should be loaded from an environment variable or passed as an argument and not hardcoded
  * depending on the dataset, it should include a way to check if a file needs updating. This can be achieved by checking the local and remote last modified date and/or checksum, depending on what information the remote server shares. If it is not possible to get either of these from the remote server than it is useful to create a file listing them as they are locally after the first download. This can then be used as reference.  

Finally, some servers offer APIs or can generate a code based on a specific request. While these are usually not sufficient to handle the full download, they provide a useful starting point.

```{warning}
Always have the code under version control!
```

## File and directory organisation

While all the generic advice on [how to organise and name files](../tech/drs.md) is still applicable, when replicating a dataset it is important to also consider the original data organisation. 

### Naming files

In most cases there is no need, and in fact it is not a good idea, to rename the files. The only exception is for datasets that are downloaded "by request", an example of these is the ERA5 reanalysis distributed by the Copernicus Climate Data Store, this data exists on the remote server as a `cube` that can be sliced by submitting a request via their API. The resulting file will have a randomly generated name, or a name specified by the user in the request.
In such case it is useful to use the API syntax, as variable, resolution, data product and others characteristic will be defined in the API by a DRS.

### Directory organisation

Similarly, if the original data is organised in directories already, the first choice should be to replicate this structure. This will make it easier to run future updates and compare what is available remotely and locally.
However, there are some exceptions when it is sensible to modify or adopt a different directory structure.
 * one obvious case is the one illustrated above where a directory structure doesn't exist to start with
 * if the data distributors dumped all the files in one directory depending on the number of files and their homogeneity it might be useful to subset them, for example by year or by variable.
 * some datasets are updated daily, often big collection of satellite data or observation follow this pattern. In such cases the files often include only one or few timesteps, resulting in a huge number of files which make accessing the data inefficient. Then it is reasonable to concatenate the files in daily or monthly units.
 * it is also important to consider how the data will be accessed or used locally. If it will be mostly access following an established workflow then it is sensible to adapt the directory structure to this workflow. On the contrary if a flexible access option is available to the users, i.e., a database or catalogue such as Intake that made the exact location of the files redundant, it might be advantageous to follow the original data directory structure as closely as possible. 

