# Backup checklist

## How essential is the data - does it have to be backed up?
* Intermediate output, run logs
    * Not useful once an experiment is finished
* Processing scripts
    * Useful to reproduce an experiment but could be redone
* Model input
    * Essential to reproduce an experiment
* Ease of reproducing the data
    * observations cannot be recreated
    * some input data might be available elsehwere but difficult to obtain 
    * can be reproduced but slow and cpu consuming process
    * easy to reproduce: backup code/workflow
* Published results
    * they should be backed up, check what is repository strategy
    * data underlining publications or a PhD thesis has to be available in case of legal dispute for  5 years from publication
* Database
    * usually hard to rebuild but small enough to be backed-up frequently
* Number of people accessing the data
    * just you, your group, people from around the world
    * this is particularly important if you are maintaining a web service via cloud, you should make sure you can recover your instance quickly and resume the service with the minimum interruption


## How big is the data?
* Text files - Source code, scripts, configuration files, small data files
    * Sizes < 100 MB
    * Not suitable for archives unless bundled into a tar file
    * source code and other text files can be kept under version control
* Data files - (for example netCDF) 
    * 1 GB to 100's of GB
    * archive systems like tape are specifically designed for this
## How often is updated?
* Unchanging once produced - e.g. raw model output
    * Tape archives
* It is updated and reviewed occasionally but not too frequently: post-processed output
    * external drives, cloud and IT services, faster to retrieve than tape
* Continually changing - source code under development
    * Use automated revision control system - subversion, git
 

## How safe is the backup system? What happens if...
* You delete a file accidentally or the local file system fails
    * Back up on a different file system
* Your storage provider goes bankrupt
    * Multiple backup providers
* A fire destroys a building
    * Offsite/multiple backups
* A flood/earthquake damages a city
    * Offsite/multiple backups with a wide separation

Check regularly logs and that you can actually recover the files!!!

## Options
* `/home` on NCI or other institution server
    * Limited space
    * Backed up - Institutions will have their own strategies
* University usually offer backup option on shared drives for data on your laptop
    * reasonably large, but not suitable for huge amount of data
    * quick to retrieve
    * easy to automate
* Tape archives/ Data repositories
    * Designed for archiving large and/or important data sets
    * Will have their own backup strategies - e.g. NCI tape is duplicated to two separate buildings at ANU
* USB external hard drive
    * Simple way to have a separate backup, cheap
    * Can manage history manually or with something like time machine
    * Not suitable for long-term storage - disks have limited lifetime
* Cloud storage, e.g. Dropbox, google drive, Github
    * Can access from anywhere
    * Offsite backup
    * Can set up folders to automatically be backed up
    * Is the service still going to be there in 5 years?
    * Git and GitHub, and other version control services, are only suitable for text files, not binary, so they are usually ok for code or readme files not for the actual data
    * NB some institutions might limit what services you can use based on security issues
* snapshot of instances for VMs on [Nectar](https://support.ehelp.edu.au/support/solutions/articles/6000085112-backing-up-data) and NCI clouds
