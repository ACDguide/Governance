# Project management

Note, this is NCI specific content - on CSIRO internal resources e.g., access mgmt is governed by windows ACLs - email schelp for advice.
Project handling   
On the NCI server disk allocations are managed via projects. Any dataset will be associated to a project, ideally this should be a data specific project, i.e. a project set up to share one or more datasets. It is not ideal to share data via a computational project as this usually are organised by users and have less restrictive permissions.
If this is unavoidable and the data is hosted on a project with multiple uses, then try to separate the working area from the data collection part.

## proposing a new project

https://opus.nci.org.au/display/Help/How+to+propose+a+new+project

## Mancini or my.nci.org

[Mancini](https://my.nci.org.au/mancini/login?next=/mancini/) is the web interface NCI uses to manage account and allocations. Any NCI users can access it to manage their project memberships. If you are managing a project you gre listed as Lead CI and get access to some extra features.
First of all as well as invite and/or accept new members you can promote one or more users to 

Researcher
Ordinary project member. Cannot alter other memberships.
Chief Investigator (CI)
Can approve and reject project membership requests. Can delete "researcher" memberships.
Delegated Lead CI
Same as CI but can also promote other members to CI role, demote CIs, and delete CI memberships. Receives email alerts for membership requests.
Lead CI
Project leader. Can approve, reject, promote, demote and delete all project memberships. Only receives email alerts for membership requests if the project has no delegated lead CIs

## Writers' group
If you're project is a specific data project you can ask NCI to create an associate writers group, if a project is labelled as `ab12` the associated writer group is `ab12_w`.
Having two separate groups allows 

##  Use of posix permissions

## Use of ACLs
  caveats with ACLs - what breaks them and when do they break?

## Accounting
Covering the accounting tools available to handle storage allocations at NCI is behind the scope of this guidance, but you can refer to [this blog from the CLEX CMS]() to get an overview.
