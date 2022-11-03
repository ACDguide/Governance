# Guidelines to create a climate dataset

## UNDER DEVELOPMENT

## Scope of the guidelines

These guidelines cover the various aspects of creating robust and well-described climate data for reuse, analysis, sharing, and publication.

We have identified four primary use cases that guide the recommendations and requirements you should follow when creating your climate datasets:  
1. for your own reuse and analysis (basic dataset needs)  
2. sharing with colleagues for collaboration (minimum sharing recommendations, no citation necessary)
3. for publication alongside a research paper (journal requirements apply)
4. for publication into a large multi-institutional intercomparison project like CMIP (strict standards apply)

Additionally, we have identified two main situations you may find yourself in: i) preparing your datasets from scratch (i.e. you have 'raw' data that is currently undescribed, and in a format that is not analysis-ready); or ii) deriving metrics or indices from a reference dataset (e.g. performing an analysis on CMIP data for a research publication). We will mostly be discussing the first situation where you are creating climate data from scratch, with specific recommendatations for the second situation later in the section.


## Index
* [Dataset creation basics & sharing recommendations](create-basics.md)  
This is an overview of the landscape of climate datasets, including the various components of netCDF files and their storage in POXIS systems, and some best practice recommendations for backuping up data and management of the creation process.  

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
* [Requirements for publication](create-publishing.md)  
This chapter outlines the standards for publication data that either accompanies a journal article or is submitted to an intercomparison project (e.g. CMIP), and some recommendations for tools to aid this process.
    
    * Publishing in a journal
    * Submitting to an intercomparison project

&nbsp;
* [Checklists for data management in the project lifecycle](create-checklists.md)
