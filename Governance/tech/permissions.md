# File permissions

Access to files and directories is controlled by setting permissions, on a UNIX system the base permissions are set using POSIX and can be extended with Access Control Lists (ACLs). 

(posix)=
## POSIX
Most UNIX file systems use the Portable Operating System Interface (POSIX) to control who can access files and directories. POSIX uses a combination of three groups of users, known as `access classes`:
 - `user` each user identified by a user-id
 - `group` a group of users identified by a group-id, on NCI groups are usually associated to a project, and occasionally to a specific role
 - `other` the definition of this class depends on each file/directory context, as it represents anyone else who is not the user or a member of the group.

Each file or directory is owned by only one user and one group, only the owner or a system administrator can change its permissions.

There are three kinds of permissions:
 - `read` - the permission to read a file. When set for a directory, only names of files in the directory can be listed, other details like file type, size, ownership, permissions etc. are not visible.
 - `write` - the permission to modify or remove a file. When set for a directory, it grants the ability to modify entries in the directory, including creating, deleting, and renaming files. Note that, without execute permission on a directory, the write permission does not take any effect.
 - `execute` - the permission to execute a file. When set for a directory, it is interpreted as the search permission: it grants the ability to access file contents and meta-information if its name is known, but does not list files inside the directory, unless read is set.

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

NB When listing a directory content with `ls -l`, an additional “+” character is displayed after the permissions of all files that have extended ACLs (see below for more information).
````
 
### Hidden permissions

Most of this section is taken from the [NCI user guide](https://opus.nci.org.au/display/Help/File+Access+Permissions).

In addition to the 9 bits required to store the user, group, and other permissions of a file, there are three kinds of "additional permissions" that are rarely used but are extremely important to understand. The additional permissions are known as the `setuid bit`, `setgid bit`, and `sticky bit`. Each special bit has a different function depending on where it is used.

**setuid**

The setuid bit on an executable file means that the file will run as the userid of the file's owner as opposed to the userid of the user executing the file. 
It is considered as a security hazard and will have no effect when setting the execute bit to `s` in the user owner triad on Gadi.

**setgid**

The setgid bit is similar to the setuid bit but set the permissions for its group owner. It enables a command to be run as the project that owns the file rather than the user's default project. On Gadi, again, for security concerns, it is ignored when set on standard files, but it can be used on directories to force new files and directories created inside them to inherit their group ownership.

```{code}
chmod g+s / g-s 
```

**sticky bit**

When a directory has the sticky bit set, its files can be deleted or renamed only by the file owner, directory owner and the root user. The command below shows how the sticky bit can be set.

```{code}
chmod +t / -t
```

This is useful to keep writing permissions for anyone in the group but avoid someone accidentally deleting a file they don't own.

**umask**

The default permission for newly created files is set in the umask value. On Gadi, `umask 022` is the default configuration in the system `.bashrc` file. Users can overwrite it in their own file ~/.bashrc. 

The command `umask` sets the inverse mask of the default file access permissions. The OS restricts the permissions of newly created files to no more than the defined permissions by the umask value. 

```{note}  **What happens when a file is created on Gadi**

Every time a new file or directory is created, the first set of permissions is automatically created based on the user who created them and their account settings.
- all project's folders have `rwxrws---` permissions, hence a user has to be part of the group to read/write in them. The `s` in the group execute position shows that the setgid is active, so any new file will inherit the directory group rather than the user group
- the owner of the file is the user who first creates the file
- if the file is created in \$HOME then the file group will be the user\$PROJECT, this is usually set in \$HOME/.rashrc
- the permissions of the file are determined by the umask file
- if a file is created by running a program with active setuid and setgid, then they will determine the permissions
- if the file is in a directory with the `sticky bit` activated, then only the file owner, directory owner or root will be able to remove the file, regardless of other permissions.
```

### Changing permissions

A file/directory owner is the only user that can set and change a file's permissions and/or group (aside from a system administrator). 
Unix commands are:
* `chmod` to change permissions; 
* `chgrp` to change group `chgrp`;
* `chown` to change owner.

```{warning}
`chown` can only be used by an NCI system administrator. A request can be made to the NCI helpdesk and both the current and new owner should be cc-ed, occasionally NCI might also request the Lead CI of the project to authorise the transaction. 
```

In most cases just using the POSIX permission system is sufficient to handle who can view or write a specific file. The limitations of this system are obvious when there is the need to set different levels of permissions for different groups of users. 
In that case, the distinction between `other` and `group` might not be sufficient.

An example of this is when managing a data collection at NCI. NCI policy dictates only users in the group can view a project's files. It is not allowed to have an `other` reading permission at the main project directory level.
This means that it is not possible to have only a subset of the group users (i.e., the data managers) having writing permission.
This is where Access Control Lists (ACLs) enter into play, as with ACLs is possible to set permissions for a different group and/or user.
In the data management context this usually happens by setting a writers group which can be joined by all the managers and then using ACLs to give this group writing permission.

(acls)=
## Access Control Lists
[Access Control Lists](https://www.redhat.com/sysadmin/linux-access-control-lists) (ACLs) are used to impose a finer level of permissions control on files and directories.

### ACLs cheat sheet

````{dropdown} **Listing ACLs: getfacl**
```{code}
getfacl <file/dir>  
```
Shows *file/dir* ACLs. If ACLs are set, a line like “mask::r-x” should be present.
`ls -l dir`  should also show a '+' at the end of permissions if ACLs are set
Eg.  drwxr-s---+ 

```{code}
getfacl -h
```
Display help

```{code}
getfacl -a somedir
```
Display the ACLs for files in *somedir* only

```{code}
getfacl -d somedir
```
Display the default ACLs for *somedir* only

`u` for user
`g` for group
`o` for others as in the usual permissions

```{code}
getfacl --omit-header somedir
```
Will show only the actual permissions and not the header showing owner, group and flags

````

````{dropdown} **Setting ACLs: setfacl**

```{code}
setfacl -h
```
	Display help

```{code}
setfacl -m u:user1:r-x  onefile  
```
Give *user1* r-x access to *onefile*,
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

````{dropdown} **Removing ACLs**

```{code}
setfacl -x u:user1 somedir
```
Remove all ACLs for *user1* in *somedir*

```{code}
setfacl -b somedir
```
Remove all ACLs for directory *somedir*

```{code}
setfacl -k somedir
```
Remove all default ACLs for directory *somedir*
````


````{dropdown} **Backing up and restoring ACLs**

```{code}
getfacl -R somedir > somedir_acls
```
Save ACLs directive for *somedir* to *somedir_acls* file

```{code}
setfacl --restore=somedir_acls
```
Restore ACLs directives for *somedir* from the *somedir_acls* file
````

```{warning}
Only the file/directory owner can change ACLs, as for any other permissions. If a user runs this command on a directory containing some files they do not own, they will get a warning like “Operation not permitted”. These warnings can be safely ignored, if there are files that they own, the ACLs will be successfully updated for these.
```

### Troubleshooting

ACLs are very useful but tend to get broken easily. 

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
The first three lines refer to the normal POSIX permissions, in this case we can see that pxp581 is the owner, ua8 the group and that this directory has setgid (flag: s) set. So, any new file in it will belong to ua8 too.

The next 5 lines show the POSIX permissions (user, group and other), a permission for user ua8_nfs to `rwx` set by ACLs and the mask also `rwx`.
What the `mask` does is to set the upper boundary of what permissions can be.
It affects only the permissions of the group and/or any extended user and group added by ACLs. The mask has no affect on other or the main user permissions.
However, as the directory has setgid, set the directory other permissions act as a mask for the file other permissions. So, if a file with write permissions was copied in here, the new file will still have only `r-x` permissions, as the file can't get more permissions on 'other' than the directory other r-x permissions.

```{admonition} **Order of operations**
When a process requests access to a file system object, two steps are performed.
1. The ACL entry that most closely matches the requesting process is selected. The ACL entries are looked at in the following order: owner, named users, (owning or named) groups, others. Only the highest ranking entry determines access: i.e. if the user is the owner this will have precedence on the group permissions. 
2. The system checks if the matching entry contains sufficient permissions to execute action.
```

The effective permissions are set to the permissions defined in the `mode`, minus the permissions set in the current `umask`. However, the `umask` has no affect if a default ACL exists. 

The mask entry is automatically created when needed but not provided. Its permissions are set to the union of the permissions of all entries that are in the group class, so initially the mask entry does not mask any permissions.

Here is an example of 'broken' ACLs:
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
As some process has set the `mask` to `rw-`, the group will have effectively `r--` instead of `r-x` permissions. And similarly, the groups w40 and hh5_w ACL entry contains permissions that are disabled by the mask entry, so `getfacl` adds a comment that shows the effective set of permissions granted by that entry.<br>
If we grant again writing permissions to the group using `chmod` the mask will change, and the ACLs will be again effective. The ACLs can be disabled but not altered by `chmod`.

Any command that sets the `mode parameter` can have unexpected effects on ACLs. Aside from `setacls` and `chmod`, these are usually commands used to create, move, and copy files. 

```{dropdown} **mkdir**
Unless otherwise specified, the `mkdir` command uses a value of 0777 as the mode parameter to the `mkdir` system call, which it uses for creating the new directory.
This corresponds to `a+rwx,ug-s,-t`. 

If this is run in a directory with ACLs set, all permissions not included in the mode parameter are removed from the corresponding ACL entries, but there is no noticeable affect because the value 0777 used for the mode parameter represents a full set of permissions.
```

````{dropdown} **cp**
`cp` will preserve the permissions of the original file, but it will change the group depending on the setgid bit of the destination folder.

As an example:
```{code}
cp test.txt /g/data/ua8/.
```
the new test.txt file in ua8 will keep the same set of permissions of the original but with the ua8 group.

Using the archive flag `-a`:
```{code}
cp -a test.txt /g/data/ua8/. 
```
the new test.txt file in ua8 will preserve the same set of permissions and group of the original file.

Adding the ACLs in the mix:

```{code}
setfacl -m d:u:ua8_nfs:rwx Test
```

the full set of permissions for the Test folder is now:
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

A new test.txt file with group w40 and `rwx` only for the owner pxp581 is created and then copied to Test:
```{code}
cp test.txt /g/data/ua8/Test/.
```

The resulting permissions for the copy are:
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
The group changed to ua8 as expected but the original file POSIX permissions are setting a mask to `---` which gets mapped to the ua8_nfs user and the group permissions.

Finally, in the case the file to copy has ACLs set, running `cp -a` will preserve the permissions in the copy regardless that the destination has or not ACLs set.
Without the archive flag, the copy will lose all the ACLs and its permissions will be set depending on the directory settings.  

````

`````{dropdown} **mv**
Move (mv) behaves as an attribute-preserving copy followed by a deletion (rm), as far as permissions are concerned.
```{code}
mv test.txt /g/data/ua8/.
```
 test.txt file will retain both permissions and group without need of specifying any mode preserving flag. 

````{warning}
So, after moving files to a new project, it's a good idea to run
```{code}
 chgrp <new-project-id>
```
 on all files that have been moved.
````

Moving a file to a directory with ACLs, for example Test from the copy example:
```{code}
mv test.txt /g/data/ua8/Test/.
```
will produce the same effective permissions, as it will retain completely the permissions and group of the original file, basically ignoring the ACLs completely.

```{code}
# file: test.txt
# owner: pxp581
# group: w40
user::rw-
group::---
other::---
```
Finally, in the case the file to move has ACLs set, running `mv` will preserve the permissions regardless of the destination ACLs set (or not set).

```{warning}
Moving a file across the same file system means removing its directory entry from its containing directory. The writing operation affects the directory, not the file itself, hence no write permissions on the file are necessary to move it!
```
`````

````{dropdown} **rsync**
`rsync` will behave similarly to `cp` when run without any flag. So, if the ACLs are set on the destination, the files will inherit them.
Like `cp` rsync has an archive flag `-a` which should preserve both permissions and group.
Differently from `cp`, if ACLs are set, even when using the archive flag, the permissions and group **will not be preserved**. The `archive` flag, as well as the `perms` and `group` flags, are ignored if there are ACLs.

If rsync-ing a directory with ACLs set, as Test in previous examples, to a directory with no ACLs:
```{code}
rsync -r Test Test-no-acls/. 
```
The original directory ACLs are completely ignored, the same happens for the files contained in it.
To preserve them rsync has a specific flag `-A`
```{code}
rsync -rA Test Test-no-acls/.
```
this will preserve the ACLs. If run with the additional archive flag `-raA`, the POSIX permissions and group will also be inherited by the new directory.


```{note}
The -A flag requires source and destination to have compatible ACL systems, when this is not the case a potential solution in rsync is to use the `--chmod` option.
From the rsync man page (in the --perms section of the manual):

>To give new files the destination-default permissions (while leaving existing files unchanged), make sure that the --perms option is off and use `--chmod=ugo=rwX` (which ensures that all non-masked bits get enabled).

NB the order of flags is important: -a, -A and so on can in fact, be used but MUST come before the --chmod flag. 
This tip is from ref (4).
````

```{dropdown} **touch**
The touch command passes a mode value of 0666 to the kernel for creating the file. So, all classes will have `rw-` permissions and the group and ACLs extended classes will be mapped by a `rw-` mask.
```

```{warning}
Please note that if the ACLs were ignored because `mv` or `cp -a` were used, simply copying the file again with `cp` only won't preserve the ACLs, the file needs to be deleted first and then copied again.
```

```{admonition} References

1. [Andreas Gru ̈nbacher, POSIX Access Control Lists on Linux](https://www.usenix.org/legacy/events/usenix03/tech/freenix03/full_papers/gruenbacher/gruenbacher.pdf)
2. [NCI user guide](https://opus.nci.org.au/display/Help/File+Access+Permissions)
3. [RedHat guide to Linux Access Control Lists](https://www.redhat.com/sysadmin/linux-access-control-lists)
4. [rsync between ACLs incompatible systems](https://serverfault.com/questions/455111/rsynced-files-not-getting-proper-acl)
```
