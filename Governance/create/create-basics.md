# Dataset creation basics & sharing recommendations

See https://github.com/ACDguide/Governance/issues/7 for discussion and suggestions 

## File formats, metadata & coordinates
---
Claire:  
use an output format that will be readable by others - e.g. netCDF

define all relevant metadata fields - both for standards like CF and ACDD, but also any other metadata that may assist understanding data creation, reuse and attribution: implement these metadata fields in your post-processing workflow

Chloe:  

Key concepts: https://acdguide.github.io/Governance/appendix/concepts.html

Highly recommend netCDF-4, used throughout as standard (see https://acdguide.github.io/Governance/tech/data_formats.html)

Metadata technical descriptions https://acdguide.github.io/BigData/format_metadata.html

Guidance on which attributes are recommended as per cf/acdd: https://acdguide.github.io/Governance/tech/conventions.html

Keywords: https://acdguide.github.io/Governance/tech/keywords.html

CVs: https://acdguide.github.io/Governance/concepts/controlled-vocab.html, https://acdguide.github.io/Governance/concepts/conventions.html

Machine-readable metadata attributes (units, coordinates, time, fill_values)

Human-readable metadata attributes (long names, most global attrs)


## File & directory organisation
---

Claire:  
structure your output data into a navigable directory structure: not more than ~1000 files at any directory level, directory tree is meaningfully named

Paola:  
Depending on how many files you are going to produce you also want to make sure you have some directory structure implemented before the number of files become hard to track. It is always best to spearate different experiments/analysis. Also making sure to include provenance details in the file name itself reduce the risk of confusing different outputs

Chloe:  
Move DRS page https://acdguide.github.io/Governance/tech/drs.html to here?
(also https://acdguide.github.io/Governance/tech/filenames.html)


## Backups & archiving
---

Claire:  
Keep only sharing data in common space, tar and archive ancillary data (model input/config files etc)

Make a backup of your dataset (particularly at NCI, note the /g/data system IS NOT backed up)

Paola:  
Set up a backup strategy (could be part of DMP planning phase)

Chloe:  
Backups: https://acdguide.github.io/Governance/tech/backup.html, https://acdguide.github.io/Governance/tech/backup-checklist.html, https://acdguide.github.io/Governance/tech/massdata.html


## Data management plans & documentation
---

Claire:  
pick your project: ensure files are created belonging to the correct project, or if they need to be moved after creation, ensure that the correct group and permissions are inherited in the destination (See also ACLs page)

Create a README at the top level with information about the dataset, when it was created, who to contact, how to use etc as relevant

Make a data management plan, and consider how your data is to be shared and/or published.

Paola:  
DMP including basic info as backup, input files, tools used, license of what is used and potential output. This ideally should be part of project planning but might still be worth mentioning it here

Keep track of changes, workflow etc from the start, even if just in a simple notes text file. Make sure it is regularly updated and details are added accordingly with phase of project, in particular when starting to share data.

Chloe:  
DMPs: https://acdguide.github.io/Governance/concepts/dmp.html

Licensing https://acdguide.github.io/Governance/concepts/license.html


## Code management & version control

Claire:  
If your data is an analysis product, keep the code nearby the data or document where it can be accessed (snapshot the version of the code used to create this dataset)

Paola:  
Keep code under version control

Chloe:  
Versioning: https://acdguide.github.io/Governance/tech/versioning.html
