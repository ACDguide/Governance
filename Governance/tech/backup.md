# Backup strategy

A large amount of a researcher's time is spent in the production and manipulation of data. No technology is perfect, and data loss can happen, from losing your computer, to a hard drive failing or just deleting the wrong directory. No-one wants to lose data; results can be costly or even impossible to reproduce. It is important to have some idea of how you could recover them if something were to happen to your files. Consider also situations in which the data is not irretrievably lost but might not be available for a while, this could be an issue if you have a deadline to meet.

## Have a recovery strategy worked out
You do not have to, but it might help writing down your backup strategy, both to make sure you included everything and to remember what you did for particular files. State how often the data will be backed up and to which locations. This will be probably be different depending on the kind of data. How many copies are being made?

Add details on how to recover the files, it is easy to forget and if there are logs created from the backup action where they are located.

### What is essential?
The first thing to consider is which part of your data is essential to have, especially when you have a lot of it. You may want to preserve output files from a very long simulation, but not care about the log files once you have verified your results. Or perhaps you have collected observations, and these cannot be reproduced. Particularly if they are observations of a rare phenomenon. The scripts to create all the plots used in your latest paper can probably be reproduced but with lots of time and effort. 

Also think about who else might be making use of your files, are other people using your results in their own research projects?

### What data is most vulnerable?
Not all the storage we use is identical, it is more likely to have a hard drive failure on your laptop then on one the supercomputer or university drives. They used hard drives that partially protect from data loss. Some services might be more reliable than others, including backup services. Make sure you know the characteristic of the storage you are using or intend to use, check if it is already backed up. Consider also that technology changes and hard drives deteriorate with time, so the age of the storage you used is also a factor to consider.

If you are you using files managed by others, make sure you know how they are managed. If they are likely to be removed and if they are backed up.

### What are you protecting against?
Apart from data loss you might also be concerned about your data being unavailable. Similarly, you might want to retrieve older versions of files, this is usually more likely for documents and code. If you have completed a project a need to preserve the data then what you really thinking of is archiving which is a different process, then you should look at archiving options. 

### How big is your data?
The next thing to consider is how big your data is. Your home directory can easily be backed up to a portable hard drive or to Dropbox, this is not really an option when you have terabytes of model output. However, supercomputer providers use a tape data archive, known as MDSS at NCI, to archive large files. Most institutions also have their own archives for important data created by their researchers. 

### How often do you update your data?
You should also think about how often the data changes, this will determine how often you will need to back it up. Codes change often and using a version control system is the only way to really keep track of all the versions. Similarly, you might want to automatically update your documents on a daily basis. Model output or recorded observations are unlikely to change, you might need to back them up only once. Post processed output will change more frequently while you are still conducting your analysis, it might be worth to have some level of automation and back up your files every few days.

### Characteristic of different backup options
Not all backup solutions provide the same protection. Creating a copy of a file in a separate directory on your computer provides a measure of protection against accidental deletion, however it could be lost if your hard drive fails. On the other end of the scale you could store copies of your data on archival tapes in different cities, so that it could still be recoverable in the case of natural disasters. Generally, the latter is costly for a large data set, the amount of protection needed should be balanced against the value of your data.

### Set up regular checks
Backup automated jobs can also fail, so make sure regularly you can access your backed-up files and they are getting updated as expected. A server restart could stop your cronjob from happening, changes in permissions might make the backup fail. If the backup has logs check them for error and fix them asap.

## What backup options are available?

###University IT services

Most universities will provide shared storage on their local network that can be used to setup automatic backups. These services are robust and properly managed storage, so they are an excellent choice. You can easily select files from your laptop to backup and is usually fast to retrieve them should you need to. This is also useful if you are switching to a new computer. Check what is already being backed up by your local IT support, they may be backing up some part of their servers by default. For instance, NCI backups user home directories on their servers.

### Tape and other institutional data repositories

For anything which is really big, which is quite common in climate science, you can use tape. This is less accessible then other options, but it has a large capacity and it is optimised for storing large files. Tape is also a good choice for archiving however, you should make sure this is its intended use. You can learn more how to do so in the [massdata page](massdata.md).

### Institutional or discipline data repositories

These are not, strictly speaking, backup services but if you have a finished data product this might be suitable for preservation. Ask your institution's data services about archiving services available to store large data sets. These services have their own data management plans in place to ensure the integrity of data, you may need to provide a data management plan describing the value of the data & how long it needs to be stored for. Similarly publishing your data and making it available is a good way to preserve it as well as sharing it.

### External hard drive

Get an external hard drive at least as big as is in your computer, then either set up a cron job to automatically rsync your internal and external hard drives on linux or enable time machine if you use a mac. This gets you a backup of your whole workstation that you can use to recover all your installed programs and local data if a hard drive fails.

### Cloud

You can also use a service like dropbox, google drive to automatically back up your home directory, these services limit the space you can use, however they provide a remote backup and allow you to access files from anywhere.

### Laptop

Your own laptop can be used to backup files you normally keep on the cloud or on a different server. Do this only for relatively small amount of data. If you want to keep extra copies of a code also using a shared server is fine. Do not use storage on disk at NCI or another server, or Nectar cloud resources to backup big amounts of data!! Storage is allocated to projects and it is shared on these servers and backup is not a good way to use this resource. 

### Snapshots for VM instances

If you are managing cloud servers via NCI cloud or Nectar, take regular snapshots of your instances. It is not unlikely to bump into issues when updating a VM, and it is really useful to be able to restart your instance from a working state.

### Version control

Version control is a must for your code and for any text files, as they change frequently, and you might want to recover older versions. It is not a good option for data files as they are usually binary. However, you can use it to keep track of changes to your data by using it for readme files describing your workflow. Here you can learn more about git and GitHub 

