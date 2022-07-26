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
The setuid bit on an executable file means that the file will run as the userid of the file's owner as opposed to the userid of the user executing the file. 
It is considered as a security hazard and will have no effect when setting the execute bit to `s` in the user owner triad on Gadi.

*setgid*
The setgid bit is similar to the setuid bit, but set the permissions for its group owner. It enables a command to be run as the project that owns the file rather than the user's default project. On Gadi, again, for security concerns, it is ignored when set on standard files but it can be used on directories to force new files and directories created inside them to inherit their group ownership.

chmod g+s / g-s 

**sticky bit**
When a directory has the sticky bit set, its files can be deleted or renamed only by the file owner, directory owner and the root user. The command below shows how the sticky bit can be set.

chmod +t / -t

This is useful when you want to keep writing permissions for anyone in the group but avoid someone accidentally deleting a file they don't own.

**umask**
The default permission for newly created files is set in the umask value. On Gadi, `umask 022` is the default configuration in the system .bashrc file. User can overwrite it in their own file ~/.bashrc. 
umask
The command `umask` sets the inverse mask of the default file access permissions. The OS restricts the permissions of newly created files to no more than the defined permissions by the umask value. 

### What happens when a file is created on Gadi

Everytime a new file or directory is created the first set of permissions is automatically created based on the user who created them and they their account settings.
- all project folders have `rwxrws---` permissions, hence you have to be part of the group to read/write in them. The `s` in the group execute position shows that the setgid is active, so any new file will inherit the directory group rather than the user group
- the owner of the file is the user who first create the file
- if the file is created in $HOME than the file group will be the user $PROJECT, this is usually set in $HOME/.rashrc
- the permission of the file are determined by the umask file
- if a file is created by running a program with active setuid and setgid, then they will determine the permissions
- if the file is in a directory with the `sticky bit` activated then only the file owner, directory owner or root will be able to remove the file, regardless of other permissions.


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

```{code}
getfacl --omit-header somedir
```
will show only the actual permsisions and not the header showing owner, group and flags

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
-m stands for `modify`

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

Let's see first how to interpret the `getfacl` output
```{code}
getfacl Download/
# file: Download/
# owner: pxp581
# group: ua8
# flags: -s-
user::rwx
user:ua8_nfs:rwx
group::r-x
mask::rwx
other::--x
default:user::rwx
default:user:pxp581:rwx
default:group::r-x
default:mask::rwx
default:other::r-x
```
The first three lines refer to the normal posix permissions: in this case we can see the pxp581 is the owner, ua8 the group and that this directory has setgid (flag:s) set. So any new file in it will belong to ua8 too.
The next 5 lines show the posix permissions (user, group and other), a permission for user ua8_nfs to `rwx` set by acls and the acls mask also `rwx`.
What the `mask` does is to set the upper boundary of what permissions can be.
It has effect only on the permissions of teh group and/or any extended user and group added by acls. The maks has no effect on `other` or the main `user` permissions.

Here is an example of 'broken' acls:
```{code}
# file: test.txt 
# owner: pxp581
# group: hh5
user::rw-
group::r-x			#effective:r--
group:w40:rwx			#effective:rw-
group:hh5_w:rwx			#effective:rw-
mask::rw-
other::r--
```
As some process has set the `mask` to `rw-`. The group will have effectively `r--` instead of `r-x` permissions. And similarly the groups w40 and hh5_w

Commands that have effects on acls (aside form setacls) are
chmod

The effective permissions are set to the per- missions defined in the mode parameter, minus the per- missions set in the current umask.
The umask has no effect if a default ACL exists. 

A process requests access to a file system object. Two steps are performed. Step one selects the ACL entry that most closely matches the requesting process. The ACL entries are looked at in the following order: owner, named users, (owning or named) groups, others. Only a single entry determines access. Step two checks if the matching entry contains sufficient permissions

The access check algorithm can be described in pseudo-code as follows.
If the user ID of the process is the owner, the owner entry determines access
else if the user ID of the process matches the qualifier in one of the named user entries, this entry determines access
else if one of the group IDs of the process matches the owning group and the owning group entry contains the requested permissions, this entry determines ac-
cess
else if one of the group IDs of the process matches the
qualifier of one of the named group entries and this entry contains the requested permissions, this entry determines access
else if one of the group IDs of the process matches the owning group or any of the named group en- tries, but neither the owning group entry nor any of the matching named group entries contains the re- quested permissions, this determines that access is denied
else the other entry determines access.
If the matching entry resulting from this selection is the owner or other entry and it contains the requested permissions, access is granted
else if the matching entry is a named user, owning group, or named group entry and this entry con- tains the requested permissions and the mask entry also contains the requested permissions (or there is no mask entry), access is granted
else - access is denied.

The mask entry is automatically created when needed but not provided. Its permissions are set to the union of the per- missions of all entries that are in the group class, so the mask entry does not mask any permissions.

An additional “+” character is displayed after the per- missions of all files that have extended ACLs.

The group class permissions can be modified using the setfacl or chmod command. If no mask entry exists, chmod modifies the permissions of the owning group en- try as it does traditionally. The next example removes write access from the group class and checks what hap- pens.

As shown, if an ACL entry contains permissions that are disabled by the mask entry, getfacl adds a comment that shows the effective set of permissions granted by that entry. Had the owning group entry had write access, there would have been a similar comment for that entry. Now see what happens if write access is given to the group class again.
After adding the write permission to the group class, the ACL defines the same permissions as before taking the permission away. The chmod command has a nonde- structive effect on the access permissions. This preserva- tion of permissions is an important feature of POSIX.1e ACLs.

A subdirectory inherits ACLs as shown next. Unless otherwise specified, the mkdir command uses a value of 0777 as the mode parameter to the mkdir system call, which it uses for creating the new directory.

Files created inside dir inherit their permissions as shown next. The touch command passes a mode value of 0666 to the kernel for creating the file.
All permissions not included in the mode parameter are removed from the corresponding ACL entries. The same has happened in the previous example, but there was no noticeable effect because the value 0777 used for the mode parameter represents a full set of permissions.
No permissions have been removed from ACL entries in the group class; instead they are merely masked and thus made ineffective. This ensures that traditional tools like compilers will interact well with ACLs. They can create files with restricted permissions and mark the files executable later. The mask mechanism will cause the right users and groups to end up with the expected per- missions.


You need to be the file/directory owner to change acls, as for any other permissions. If you run this command on a directory that contains some files you don’t own you’ll get a warning like “Operation not permitted”. You can safely ignore these warnings, if there are files that you own, the acls will be successfully updated.


rsync

cp/mv
cp will preserve the same permission of the original file but it will change the group if you are copying a file from
cp test.txt /g/data/ua8/.
the new test.txt file in ua8 will keep the same set of permission of the original but with the ua8 group
To preserve the permission you need to sue the `archive` flag `-a`
cp -a test.txt /g/data/ua8/. 
the new test.txt file in ua8 will keep the same set of permissionis and group of the original file

mv test.txt /g/data/ua8/.
and test.txt file will retain both permissions and group without need of specifying 

so after movi9ng files to a new proejct you should be running chgrp <new-project-id> on all files you moved

Let's try to add now acls in the mix

setfacl -m d:u:ua8_nfs:rwx Test

These will be the full set of permissions for the new Test folder
```{code}
getfacl --omit-header Test/
user::rwx
group::r-x
other::r-x
default:user::rwx
default:user:ua8_nfs:rwx
default:group::r-x
default:mask::rwx
default:other::r-x
```

I create again a test.txt file with group w40 and rwx only for the owner pxp581

and then
cp test.txt /g/data/ua8/Test/.

these are the resulting permissions after copying the file
```{code}
# file: test.txt
# owner: pxp581
# group: ua8
user::rw-
user:ua8_nfs:rwx		#effective:---
group::r-x			#effective:---
mask::---
other::---
```
The group changed to ua8 as expected but the original file posix permissions are setting a mask to `---` which gets mapped to the ua8_nfs user and the group permissions.

mv test.txt /g/data/ua8/Test/.

will produce the same effective permissions, as it will retain completely the permissions and group of the original file, basically invalidating the acls completely.
This is because mv does not make a copy of the file and remove the original, unless you're moving the file between different filesystems. mv moves the file.
```{code}
# file: test.txt
# owner: pxp581
# group: w40
user::rw-
group::---
other::---
```

The same will happen if using `cp -a`

Please note that if the acls were ignored because `mv` or `cp -a` were used. Simply copying again the file with `cp` only won't preserve the acls, the file needs to be deleted first and then copied again.

NB also that while the group permissions get overulled by the mask the other permission will get preserved, still the directory other permissions will have an effect on the final other permissions. So for example if I add write permission to other before moving the file

chmod o+wx test.txt

ls -l test.txt 
-rw-r--rwx 1 pxp581 w40 5 Jul 22 13:09 test.txt

cp test.txt /g/data/ua8/Test/.

 Test]$ getfacl test.txt 
# file: test.txt
# owner: pxp581
# group: ua8
user::rw-
user:ua8_nfs:rwx		#effective:r--
group::r-x			#effective:r--
mask::r--
other::r-x

The mask has modified the group and ua8_nfs user permissions as expected, but not `other`. Still other doesn't have write permission as the original file and this is because the Test directory has setgid set and the file can't get more permissions on 'other' then what the directory other r-x permissions

We should have used cp -a or mv to override that


Move (mv) is essentially an attribute-preserving copy followed by a deletion (rm), as far as permissions are concerned.1 Unlinking or removing a file means removing its directory entry from its containing directory. You are writing to the directory, not the file itself, hence no write permissions are necessary on the file.

rsync will behave similarly to `cp` when run without any flag
differently from cp even if using the `archive` flag which should preserve both permissions and group with rsync. If acls are set the result will be the same with or without these flags
Also the single `perms` and `group` flags are identically ignore when run on their own.
oFinally see this:

https://serverfault.com/questions/455111/rsynced-files-not-getting-proper-acl

 "modification of the file permission bits result in the modification of the associated ACL entries" and vice versa. Because without the proper flag, rsync uses the source permissions this changes the ACLs on the target.

The solution in rsync is to use the --chmod option. From the rsync man page (in the --perms section):

To give new files the destination-default permissions (while leaving existing files unchanged), make sure that the --perms option is off and use --chmod=ugo=rwX (which ensures that all non-masked bits get enabled).


Reference:

https://www.usenix.org/legacy/events/usenix03/tech/freenix03/full_papers/gruenbacher/gruenbacher.pdf
https://opus.nci.org.au/display/Help/File+Access+Permissions
