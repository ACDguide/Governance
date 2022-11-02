# Moving data

!!!COMMENT

we should cover here commands, tools etc to move data between

## NCI-Gadi

NCI has a dedicated data-mover node that can be used to move data to/from Gadi.
To copy files to Gadi you should use the Gadi data movers gadi-dm.nci.org.au:
$ scp /path/to/local/file abc123@gadi-dm.nci.org.au:/path/to/destination/on/gadi
To copy files from Gadi:
$ scp abc123@gadi-dm.nci.org.au:/path/to/file/on/gadi /path/to/local/destination

You can also transfer data through gadi-dm.nci.org.au using•commands such as sftp, rsync,...•applications such as FileZilla, WinSCP,....•No interactive sessions on any of the data-mover nodes, try interactive copyq jobs

This page covers ssh-keys but alos how to set specila purpouse one for rsync: https://opus.nci.org.au/display/Help/Using+SSH+keys

### Moving data from different disk storage
Moving data among different storage is usually straightforward, just using
the unix `cp`, `mv`, `rsync` commands, except for massdata that has his dedicated mdss commands, covered in the [massdata page]().
However,  there are differences in the way these commands will act and some consideration on the way the storage is organised

### OOD ARE
Q: How do I rsync data to OOD?
A: You will need to set up direct SSH access as per "4. Direct SSH access", and then persuade rsync to use it. Depending exactly which versions of rsync and ssh you have installed, you may be able to use the '-e' option to rsync to specify the extra options to ssh, something like rsync -e 'ssh -J abc123@ood-vnc.nci.org.au' -av abc123@ood-vnXX:/home/123/abc123/stuff-to-copy . (where ood-vnXX is the hostname from the session card within the OOD interface, and should not have nci.org.au appended to it). If your versions of ssh and rsync do not allow this, then you should be able to edit your SSH configuration file as per 4. Direct SSH access.
oTo copy your files from OOD to ARE you need to use the scp tool.  You can either do this directly using a gadi login node (ssh command from your computer or ARE Gadi terminal app) OR as a 2 step process from your computer.
Gadi login node
Login to Gadi login node either using a native SSH client on your computer OR using the ARE Gadi Terminal app
Use the scp command to copy your required files
e.g. copy select file: 
scp -r abc123@vdi-sftp.nci.org.au:DIR/FILENAME.txt
e.g. copy all files (if you have sufficient space in your Gadi home directory):
scp -r abc123@vdi-sftp.nci.org.au:. ~/ood-home-copy
Where abc123 is replaced with your NCI username and DIR/FILENAME.txt is replace by the name of the file or directory you want to copy.
Via your computer
If you would prefer a graphical transfer method then you can install a graphical SCP client on your computer and use it to first get your files from vdi-sftp.nci.org.au and then transfer them to gadi.nci.org.au.

https://opus.nci.org.au/display/DAE/Hadoop+HDFS ???
## Pawsey
Possibly this can be used as a generic source covering sftp. scp etc
https://support.pawsey.org.au/documentation/display/US/Transferring+Files

different disks/storage at NCI/other platform
different HPC systems
from/to cloud

in the context of the kind of data movement you might have to do when managing a data collection, so (I think) we shouldn't have to cover latop to HPC, as that would be irrelevant mostly (also opening a can of worms having to cover all different OS)

How to copy from a personal computer to gadi HPC system is covered in their [main documentation](https://opus.nci.org.au/display/Help/How+to+login+to+Gadi)

Also this is only a tech reference so the context can/should be given in the managing dataset section instead

## CSIRO
Thomas parallel rsync

SPeicific tools

ACCESS-archiver
