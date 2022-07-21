# Mass Data Storage System

Massdata (Mass Data Storage System, MDSS for short) is the tape storage available at NCI. This kind of storage is intended for long term storage of large files. It is possible to retrieve data from MDSS, so this is a good place to store data that will not be required for some time, for backup, or for archiving. Each project has a directory on the MDSS, the amount of storage allocated depends on the project allocation.

## MDSS proper usage

MDSS is designed for medium to long-term storage of large files, this means it is optimised for storing big amounts of data. This means it is most suitable for:

* Files you are required to keep for a long term, like data underlining published datasets, publications, PhD thesis etc.
* Files that you or someone else are likely to reuse or analyse again in the future but not in the next few months. For example, restart files or other model output you are not immediately using should be moved from disk to massdata as soon as possible.
* MDSS is suitable for backup of big data projects, like model output which could not be backed up elsewhere.

### Preparing your data for mdss

1 Organise your files and delete anything which you will not be re-using. Do not transfer data before organising it. It is difficult to get a list of what is stored on massdata, let alone to list what is in a tarred file once it is uploaded. 
2 Big files: use tools like tar to bundle files together into archive files. Create reasonably big archive files but also think of how you might want to access the data later. There is no point of tarring together two different simulations if you would want to access them separately, as then you would need to transferred back a big amount of data you do not need. Your upload will fail if any of your files are less than 20MB or the average size is less than 250 MB.
3 Files should be group readable, with group execute permissions for directories. This helps with long term maintenance, allowing administrators to track the type and size of archived data. You can change the permissions on data you own with the chmod unix utility.

While you are preparing your data to be moved it is an opportunity to also document it, if you have not done so already. You should document what you are archiving and how you are archiving it. Even a simple readme file added to your main directory can help others and your future self. If you are archiving data underlining a publication or published dataset then it is important to have a summary of what is stored in massdata. This should be part of the [dataset management plan](../concepts/dmp.md) and/or [data availiability statement](../concepts/availability-statement.md).

Useful tools:

* TAR- to create archives cheatsheet
````{dropdown}
````

* Compressing tools

## Accessing MDSS

Massdata cannot be accessed directly via a directory path. All access of MDSS is via the command mdss.

Users connected to the project have read, write and execute permissions in the corresponding directory on mdss and so may create their own files in it.

mdss has several sub-commands and options to see all of them use either:

```{code}
  $mdss --help
```
or
```{code}
  $man mdss
```
If you don't specify a project, it will use your default project. Then you add a sub-command and the path of the files and directories you want to upload, list etc.

```{code}
mdss -P <project-id> + <sub-command> + <path>
```

Most useful sub-commands are:

```{code}
mdss put   - upload files 
mdss get   - retrieve files 
mdss ls    - list directories and files 
mdss dmdu  - get the size of a directory/file 
mdss dmls  - show what is on cache and what is on tape

NB "mdss du" will also work but only return the size of what is still cached, dmdu will give the full size of what is on tape regardless if it is cached or not.
```
Please note mdss sub-commands work only interactively or on the copyq queue. To use it on copyq remember to set the storage flag as

```{code}
-l storage=massdata/<project_code>
```

### Monitoring MDSS usage

Unfortunately, there is no command to check the usage by user-id as for /g/data and /scratch. The only way to get this information currently is to ask help<at>nci.org.au. The NCI administrators can access this information for any CI of the group.

### Transferring data to and from MDSS

NCI also supports the netmv and netcp commands to work with MDSS. These commands create a copyq job to transfer multiple files. Files can be automatically tarred and compressed as part of the copy process.

Warning: The automatic archiving and compression of these tools can use a lot of storage on /scratch if you're moving lots of data!

For more info run `man netmv`.

The CMS team has also developed a utility called [`mdssdiff`](https://github.com/coecms/mdssdiff) available from the CLEX-CMS conda environments. This utility allows users to compare the contents of the local directory and a directory under /massdata. It will also recursively update the content on the massdata directory to copy the local directory or vice versa.

### Modifications to MDSS datasets

Ask the Lead CI of the project to contact NCI at help@nci.org.au if large metadata operations are needed on massdata, such as changing ownership, project code, permissions etc. of existing datasets
