# Project management

```{warning}
Note, this is NCI specific content.
```

On the NCI server, disk storage allocations are managed via projects. Any dataset will be associated to a project, ideally this should be a data specific project, i.e., a project set up to share one or more datasets. It is not ideal to share data via a computational project as all the project users will have writing access and it would be harder to guarantee a set disk quota for the dataset collection.
If this is unavoidable, and the data is hosted on a project with multiple uses, then try to separate the working area from the data collection part.
The data files should be stored on the `gdata` disk, i.e., /g/data/<project-id>. Never use the /scratch filesystem for dataset as /scratch is only meant as a temporary filesystem with fast access, files that have not been accessed for 100 days are quarantined and eventually removed.

## Starting a new project

To start a new dedicated project write a proposal to submit to NCI, details on the procedure are available from their [online user guides](https://opus.nci.org.au/display/Help/How+to+propose+a+new+project).

### Mancini

[Mancini](https://my.nci.org.au/mancini/login?next=/mancini/) is the web interface NCI uses to manage user accounts and allocations. Any NCI users can access it to manage their project memberships. Each project as a Lead CI, who is the main responsible person, sometimes this is a high-level researcher rather than a technical person. In such cases it is possible for the Lead CI to promote one or more members are delegate Lead CIs. They will now receive membership applications and share most of the Lead CI privileges.

```{dropdown} **Project Roles**

+ **Lead CI** - Project leader. Can approve, reject, promote, demote and delete all project memberships. Only receives email alerts for membership requests if the project has no delegated lead CIs
+ **Delegated Lead CI** -Same as CI but can also promote other members to CI role, demote CIs, and delete CI memberships. Receives email alerts for membership requests.
+ **Chief Investigator (CI) - Can approve and reject project membership requests. Can delete "researcher" memberships.
+ **Researcher** - Ordinary project member. Cannot alter other memberships.
```

Mancini shows how much allocation the project is using and allows the Lead CI and delgate Lead CIs to send email to all project members. This is useful to handle important communication about the datasets, as updates, changes in their management and to communicate when a dataset is going to be retired.
 
## Setting permissions
NCI uses the [POSIX](posix) to set permissions.
By default the class `other` doesn't have access to project directories /g/data/<project-id>`. This means that every prospective data user will have to become a member of the project to access the data. 
Data projects are usually organised in two main directories:
- `admin`/`code` is the working area containing codes and logs. Only the data managers should have writing access to this, but it helps trasparency letting the users having read access. 
- `data`/`replicas` is where the actual data resides. Users belonging to the group should have `read` permission everywhere and `execute` permission for the directories (without this they wouldn't be able to access the files in the directory) 
The directory and files permissions should be carefully managed to make sure that users have access to all the data files but cannot accidentally change or remove any of them.

### Writers group
If the data is hosted in a data project it is possible to ask NCI to create an associate writers group, if a project is labelled as `ab12` the associated writers group is `ab12_w`.
This is particularly useful where there is more than one user managing the data. If there is only one data manager then having a writer group is redundant as different permissions can be easily set for the `user` and the `group`. Writer groups are meant to be used in conjunction with [Access Control List (ACLs)](acls). 
All the files should be owned by the project group with `read` and `execute` (at least for folders) permissions. The ACLs are then used to give `write` permission only to the writers group.

If not using a writer group, the same approach is possible but giving `write` permission to each manager using their username. This is less ideal as it is more likely to break the [ACLs](acls) when updating or adding new files.

{{{On CSIRO internal resources, access mgmt is governed by windows ACLs - email help for advice.}}}

## Backup
`gdata` is not backed up, if the dataset files would be difficult to retrieve, or if they are the authoritative copy, it is important to have a [backup plan](../tech/backup.md). If the files are an authoritative copy it might be worth to back up the data on a separate system. 
The only option to back up data at NCI is to use to archive the data on the tape system also known as `[massdata](massdata)`.

If the dataset are a replica and they can be easily retrieved, or are frequently changing than backing up the data might be redundant.

## Accounting
Covering the accounting tools available to handle storage allocations at NCI is behind the scope of this guidance, but you can refer to [this blog from the CLEX CMS](https://climate-cms.org/posts/2022-04-26-storage-where-what-why-how.html) to get an overview.
