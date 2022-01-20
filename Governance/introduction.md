# Introduction

This book, '**[Climate Dataset Guidelines](https://acdguide.github.io/Governance/)**', provides guidelines for creating, managing, sharing and publishing climate data. With a focus on Australian climate research it has been designed to enable a common approach across the community. Despite the focus on climate data, many of the principles and tools described within are applicable to many Earth science data applications.

These guidelines are applicable to all levels of data sharing, from peer-to-peer sharing with colleagues to full publication in a public repository. 

If you intend to share your data with colleagues for simple purposes, such as sanity checking and comparisons, some level of provenance and metadata preparation is likely to be useful, so feel free to pick and choose the parts of this book that are relevant for your use case. However, if your data is to be published or shared widely/publicly, it should follow FAIR principles and meet the minimum set of formatting and metadata recommendations as described in this book.


## Chapter index

### **[Creating climate data](create/create-intro.md)**
Creating datasets that are fit for publication can be a daunting process, with many technical aspects to consider. This chapter will outline the ways to ensure that your data meets the broad [FAIR principles](https://www.go-fair.org/fair-principles/) of data sharing, along with specific requrirements and recommendations for climate-related data that will aid in the use and reproducibility of your data by the Australian, and international, climate community.

### **[Publishing climate data](publish/publish-intro.md)**
Publishing data involves uploading them to an accessible respository, and having a persistent identifier (e.g. a [DOI](https://www.doi.org/)) attached in a similar manner to publishing a research paper. This data can then be used and references by other researchers, increasing the scientific impact your dataresearch-ready data can have. Additionally, many journals now require that data on which a paper is based be published in this manner. In this chapter, the various pathways to data publication are presented, with a focus on recommendations for those at Australian research institutions.

### **[Updating published climate data](update/update-intro.md)**
As with all scientific outputs, errors and inconsistencies can be found in climate research data, oftentimes after publication. This chapter provides guidance to the updating of published data, along with recommendations for actions that can taken prior to the initial publication (such as good versioning practices) that can make this process much easier down the line, as published data may need to updated many times in its lifespan.


### **[Retiring published climate data](retire/retire-intro.md)**
Data does last forever, usually becoming outdated or obsolete within 5-10 years; this of course is simply the nature of scientific research. In this chapter, recommendations are presented on how to go about retiring a published datase without breaking citations or removing identifiers, while retaining the value of your research data. 


## FAIR(ER) Principles
Research data that is intended for sharing should follow some general principles of data management and stewardship. The guiding principles often used in data governance are the [FAIR principles](https://www.go-fair.org/fair-principles/) of data sharing -- Findable, Accessible, Interoperable, and Reusable. An extension to these are the [FAIRER principles](https://www.spatialised.net/fairer-data/) which add Ethical and Revisable to the acronym and is described in the book ['Good Data'](https://networkcultures.org/blog/publication/tod-29-good-data/). These principles are very generalised, and it is not always easy to translate their meanings into relevant practices for climate data.

### Findable
The primary way to make a dataset findable is to mint a [persistent identifier](concepts/pids.md), such as a DOI, which provides a long-lasting reference to a digital object such as climate data. The data must then be uploaded to a searchable repository, database or data catalogue, so that the data can be found and used. This is the primary aim of the [Publishing climate data](publish/publish-intro.md) chapter of this book.

### Accessible 
Accessibility of a dataset depends on where the data is stored (e.g. is it accessible ), how it is accessed (e.g. via ftp or https), the longevity of this storage, security and authentication protocols (if relevant), and usability restrictions as dictated by the license applied to the data. What happens to a dataset at the end of it's life is also a consideration, where the accessibility principle says that metadata should always remain, even if the data no longer exists. These are considerations of the [Publishing climate data](publish/publish-intro.md) and [Retiring published climate data](retire/retire-intro.md) chapters.

### Interoperable
Interoperability refers to ability of research to easily use a published dataset, especially when using common tools and coding languages. The main ways to ensure the interoperability of your data is to make use of common and open file formats (e.g. netCDF4, grig, zarr) rather than proprietary formats or those that require specialised tools, and to apply discipline-specific controlled vocabularies (e.g. [CMIP6 CV](https://github.com/WCRP-CMIP/CMIP6_CVs)) and keywords that are easily recognisable by the community. These aspects are covered in the [Creating climate data](create/create-intro.md) and [Concepts](concepts/controlled-vocab.md). Data formats are discussed in another ACDG book called ['Big Data'](https://acdguide.github.io/BigData/data_storage.html).

### Reusable
The reusability of the data is dictated primarily by the quality of the metadata and attributes. In other words, the degree to which the metadata effectively and comprehensively describes the data determines it's reusability. Details on the provenance (origin & history) of the data are vital, including how it was created, by whom, for what purpose, and using what tools. Additionally, appropriate licensing can affect usability, as a highly restrictive or unclear license can prevent others from using the data in their own research. Finally, ensuring that the metadata and attributes are in line with discipline-specific expectations and standards. This may involve applying an existing set of data standards (e.g. the [CORDEX data standards](http://is-enes-data.github.io/CORDEX_adjust_drs.pdf)), or simply ensuring that attributes, filenaming and directory structures are likely to make sense to those using the data. Reusability is the main focus of the [Creating climate data](create/create-intro.md) chapter, while licensing is explained in [Concepts](concepts/license.md).

### Ethical
As scientists, we have an ethical obligation to do no harm through our work. When it comes to data, we should ensure that the collection, distribution and reuse of data done in a way that is respectful toward humans and the planet. Privacy is fast becoming an important factor in the collection of data of all kinds, and FAIRER data should aim to avoid violating the privacy of others. The creation, storage and use of data require energy and resources at a cost to environment, and the contributions of scientific activity to climate change and environmental degredation should be a consideration when performing science.

### Revisable
The standard definition of published data generally considers the data to be fixed -- a snapshot in time, which if improved upon will result in a new dataset with fresh considerations. However, in practice this is often not the case, where published data can require fixes or corrections (e.g. typos in the metadata), retraction and republication (e.g. due to errors in the data), or extensions (e.g. observational datasets that are regularly being updated). We provide some general guidance around this in the chapter [Updating published climate data](update/update-intro.md).
