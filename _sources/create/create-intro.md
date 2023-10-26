# Guidelines to create a climate dataset

These guidelines cover the various aspects of creating robust and well-described climate data for reuse, analysis, sharing, and publication.

We have identified five primary use cases that guide the recommendations and requirements to follow when creating climate datasets:  
1. Own reuse and analysis: basic dataset needs.
2. Sharing with colleagues for collaboration: minimum sharing recommendations, no citation necessary.
3. Publication alongside a research paper: journal requirements apply.
4. Publication into a specific project: project standards apply.
5. Productisation, including market-readiness and commercialisation: standards depend on audience and intended use.

We will mostly be discussing starting datasets from scratch from 'raw' data that is currently undescribed, and in a format that is not analysis-ready. Datasets can also be derived from existing data, as result of analysis or deriving metrics and indices from a reference dataset. We provide specific recommendations for the second situation later in the section.


## Index
* [Dataset creation basics](create-basics.md)  
An overview of the landscape of climate datasets, including the various components of netCDF files and their storage in POSIX systems, and best practice recommendations for the backup of data and management of the creation process.  

    * File formats, metadata & coordinates
    * File & directory organisation
    * Backups & archiving
    * Data management plans & documentation
    * Code management & version control 

&nbsp;
*  [New, modified, and derived datasets](create-new-derived.md)  
This is the more practical description of how to create climate datasets (generally on a HPC system). It is designed to help guide those who are creating new datasets from scratch, those who are modifying existing files, those who are deriving new information from published/reference data.  

    * Creating new datasets from raw data
    * Modifying existing files in-situ
    * Creating derived datasets from existing/published data

&nbsp;
* [Requirements for publication & productisation](create-publishing.md)  
This chapter outlines the standards for publication data that either accompanies a journal article or is submitted to an intercomparison project (e.g., CMIP), and some recommendations for tools to aid this process.
    
    * Publishing in a journal
    * Submitting to an intercomparison project
    * Dataset productisation for market-ready commercialisation

&nbsp;
* [Checklists for data management in the project lifecycle](create-checklists.md)
This page contains a useful checklist to aid in data management planning; separated according to the various stages of a project lifecycle.
