# Backup checklist

## How essential is the data - does it have to be backed up?
* Intermediate output, run logs
    * not useful once an experiment is finished
* Processing scripts
    * useful to reproduce an experiment but could be redone
* Model input
    * essential to reproduce an experiment
* Ease of reproducing the data
    * observations cannot be recreated
    * some input data might be available elsehwere but difficult to obtain 
    * can be reproduced but slow and cpu consuming process
    * easy to reproduce: backup code/workflow
* Published results
    * should be backed up, check what is repository strategy
    * data underlining publications or a PhD thesis has to be available in case of legal dispute for  5 years from publication
* Database
    * usually hard to rebuild but small enough to be backed-up frequently
* Number of people accessing the data
    * just you, your group, people from around the world
    * ensure you can recover your instance quickly and resume the service with minimum interruption - this is particularly important if you are maintaining a web service via cloud


## How big is the data?
* Text files - Source code, scripts, configuration files, small data files
    * sizes < 100 MB
    * not suitable for archives unless bundled into a tar file
    * source code and other text files can be kept under version control
* Data files - (for example netCDF) 
    * 1 GB to 100's of GB
    * archive systems like tape are specifically designed for this
## How often is it updated?
* Unchanging once produced - e.g. raw model output
    * tape archives
* Updated and reviewed occasionally but not too frequently: post-processed output
    * external drives, cloud and IT services, faster to retrieve than tape
* Continually changing - source code under development
    * use automated revision control system - subversion, git
 

## How safe is the backup system? What happens if...
* You delete a file accidentally or the local file system fails
    * back up on a different file system
* Your storage provider goes bankrupt
    * multiple backup providers
* A fire destroys a building
    * offsite/multiple backups
* A flood/earthquake damages a city
    * offsite/multiple backups with a wide separation

Check logs regularly and that you can actually recover the files!!!

## Options
* `/home` on NCI or other institution server
    * limited space
    * backed up - institutions will have their own strategies
```{admonition} To recover file on NCI /home
If you accidentally deleted files from your /home at NCI they can be recovered from daily snapshots - check the [NCI documentation](https://opus.nci.org.au/pages/viewpage.action?pageId=90308816) to see how to.
```
* Universities usually offer backup option on shared drives for data on your laptop
    * reasonably large, but not suitable for huge amount of data
    * quick to retrieve
    * easy to automate
* Tape archives/ Data repositories
    * designed for archiving large and/or important data sets
    * will have their own backup strategies - e.g. NCI tape is duplicated to two separate buildings at ANU
* USB external hard drive
    * simple way to have a separate backup, cheap
    * can manage history manually or with something like time machine
    * not suitable for long-term storage - disks have limited lifetime
* Cloud storage, e.g. Dropbox, google drive, Github
    * can access from anywhere
    * offsite backup
    * can set up folders to automatically be backed up
    * is the service still going to be there in 5 years?
    * Git and GitHub, and other version control services, are only suitable for text files, not binary, so they are usually ok for code or readme files, not for the actual data
    * NB some institutions might limit what services you can use based on security issues
* Snapshot of instances for VMs on [Nectar](https://support.ehelp.edu.au/support/solutions/articles/6000085112-backing-up-data) and NCI clouds
