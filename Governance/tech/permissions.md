# File permissions

Access to files and directories is controlled by setting permissions, on a UNIX system the base permsisions are set using POSIX and can be extended with Access Control Lists (ACLs). 

(posix)=
## POSIX
Most UNIX file systems use the Portable Operating System Interface (POSIX) to control who can access files and directories. POSIX uses a combination of three groups of users, known as `access classes`:
 - `user` each user identified by a user-id
 - `group` a group of users identified by a group-id, on NCI groups are usually associated to a project, and ccasionally to a specific role
 - `other` the definition of this class depends on each file/directory context, as it represents anyone else who is not the `user` or a member of the `group`.

Each file or directory is owned by only one `user` and one `group`, only the owner or a system administrator can change its permissions.

There are three kind of permissions:
 - `read` - the permission to read a file. When set for a directory, only names of files in the directory can be listed, other details like file type, size, ownership, permissions etc. are not visible.
 - `write` the permission to modify or remove a file. When set for a directory, it grants the ability to modify entries in the directory, including creating, deleting and renaming files. Note that, without execute permission on a directory, the write permission does not take any effect.
 - `execute` the permission to execute a file. When set for a directory, it is interpreted as the search permission: it grants the ability to access file contents and meta-information if its name is known, but does not list files inside the directory, unless read is set.

````{dropdown} **Permission example**
This is an example of what the permissions look like when we list files using the long `l` option.

```{code}
ls -l
-rw-r--r--   1 pxp581 ua8  18K May 16  2016 readme.txt
drwx------   5 pxp581 ua8  512 May 21  2020 private/
lrwxrwxrwx   1 pxp581 ua8 Sep 13 20:45 data -> /g/data/ua8/Climdex/v1-0/
-rwxr--r--   1 pxp581 ua8  171 Sep  9 09:18 loadimage.sh
drwxrwxrwx   1 pxp581 ua8  512 Sep 13 20:45 worldwriteable/
^ ^  ^  ^--- other permissions
| |  '------- group permissions
| '---------- user permissions
'------------ file type: d=directory, l=symbolic link, - means regular file
```
````
 
### Hidden permissions

Most of this section is taken from the [NCI user guide](https://opus.nci.org.au/display/Help/File+Access+Permissions)

In addition to the 9 bits required to store the user, group, and other permissions of a file, there are three kinds of "additional permissions" that are rarely used but are extremely important to understand. The additional permissions are known as the setuid bit, setgid bit, and sticky bit. Each special bit has a different function depending on where it is used:

When the the special bits are used on regular files:

**setuid**
The setuid bit on an executable file means that the file will run as the userid of the file's owner as opposed to the userid of the user executing the file. This is done to allow users to perform tasks that temporarily require the user to be someone else, such as changing passwords or restarting a service. Any program with the UID bit set must be carefully written so as to block all misuse. Innumerable vulnerabilities have stemmed from setuid root programs with security holes that allowed users to execute other commands as root.
When executing a binary that has the setuid bit enabled, it inherits the permissions set for the file owner. It is considered as a security hazard and will have no effect when setting the execute bit to `s` in the user owner triad on Gadi.

*setgid*
The setgid bit on an executable file is like the setuid bit, except that the process gains the effective group of the file's group, rather than the group of the user executing the file.
The setgid bit is similar to the setuid bit, but set the permissions for its group owner. It enables a command to be run as the project that owns the file rather than the user's default project. On Gadi, again, for security concerns, it is ignored when set on standard files but it can be used on directories to force new files and directories created inside them to inherit their group ownership.

**sticky bit**
The "sticky bit" was used in the olden days to tell the kernel to keep an executable's image in memory so that it would not have to be reloaded from disk. This was commonly done with programs such as editors that were used regularly but had a significant load time. Modern systems use the "sticky bit" for other uses.
The sticky bit sets extra permissions for others. It replaces the execute permission with t. On Gadi, it is can be used to do 'deletion protection' for public directories that you have to allow others to write. For example, when exchange data in the /scratch/public directory with users outside your project, files inside it can be deleted or renamed only by the file owner, directory owner and the root user because the sticky bit is set to `drwxrwxrwt.` on the /scratch/public directory. Similarly, when you want to share data with others inside a directory in /scratch/public, set the sticky bit to apply the deletion protection follow the last example in the next section.

**umask**
The default permission for newly created files is set in the umask value. On Gadi, `umask 022` is the default configuration in the system .bashrc file. User can overwrite it in their own file ~/.bashrc. 
umask
The command `umask` sets the inverse mask of the default file access permissions. The OS restricts the permissions of newly created files to no more than the defined permissions by the umask value. 

### Changing permissions

A file/directory owner is the only user that can set and change permissions (aside from a system administrator). 
To change permissions chmod, to change group chgrp, chown is the command to change file owner but can only be used by a NCI administrator. A request can be made to the NCI helpdesk and both the current and new owner should be cc-ed, occasionally NCI might want also the Lead CI of the project to authorise the transaction. 
In most cases just using the posix permission system is sufficient to handle who can view or write a specific file. The limitations of this system are obvious when there is the need to set different level of permissions for different groups of users. 
In that case the distinction between `other` and `group` might not be sufficient.

An example of this is when managing a data collection at NCI, by NCI policy only users in the group can view a project files. It is not allowed to have a `other` reading permission at the main project directory level.
This means that it is not possible to have only a subset of the group users (i.e. the data managers) having writing permission.
This is whereACLs enter into play, as with ACLs is possible to set permissions for a different group and/or user.
In the data management context this usually happens by setting a writers group which can be joined by all the managers and that will be assigned writing permission.
(acls)=
## Access Control Lists
[Access Control Lists](https://en.wikipedia.org/wiki/Access-control_list) (ACLs) are used to impose a finer level of permissions control on files and directories.

### ACLs cheat sheet

````{dropdown} **Listing acls: getfacl**
```{code}
getfacl <file/dir>  
```
Shows *file/dir* acls. If acls are set a line like “mask::r-x” should be present
`ls -l dir`  should also show a + at the end of permissions if acls are set
Ex.  drwxr-s---+ 

```{code}
getfacl -h
```
Display help

```{code}
getfacl -a somedir
```
Display the acls for files in *somedir* only

```{code}
getfacl -d somedir
```
Display the default acls for *somedir* only

u for user
g for group
o for others as in the usual permissions

````

````{dropdown} **Setting acls: setfacl**

```{code}
setfacl -h
```
	Display help

```{code}
setfacl -m u:user1:r-x  onefile  
```
Give *user1* r-x access to *onefile*

```{code}
setfacl -m  u:user1:rwx file,  g:group1:r-x  
```
Give *user1* rwx access and *group1* r-x access to *file*

```{code}
setfacl -m  d:u:user1:r-x  somedir  
```
Give *user1* default r-x access to *somedir*, 
any new files in *somedir* will inherit this permission

```{code}
setfacl -R -m d:u:user1:r-x somedir  
```
Give *user1* default r-x access to *somedir* and recursively to all its subdirectories 

```{code}
setfacl -L -m d:u:user1:r-x somedir  
```
Give *user1* default r-x access to *somedir* following symbolic links
````

````{dropdown} **Removing acls**

```{code}
setfacl -x u:user1 somedir
```
Remove all acls for *user1* in *somedir*

```{code}
setfacl -b somedir
```
Remove all acls for directory *somedir*

```{code}
setfacl -k somedir
```
Remove all default acls for directory *somedir*
````


````{dropdown} **Backing up and restoring acls**

```{code}
getfacl -R somedir > somedir_acls
```
Save acls directive for *somedir* to *somedir_acls* file

```{code}
setfacl --restore=somedir_acls
```
Restore acls directives for *somedir* from the *somedir_acls* file
````

### Troubleshooting
ACLs are very useful but tend to get broken easily 

You need to be the file/directory owner to change acls, as for any other permissions. If you run this command on a directory that contains some files you don’t own you’ll get a warning like “Operation not permitted”. You can safely ignore these warnings, if there are files that you own, the acls will be successfully updated.


rsync

cp/mv

