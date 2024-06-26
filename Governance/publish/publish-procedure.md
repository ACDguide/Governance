# Publishing procedure

While the exact procedure to publish a dataset will depend on where the data is published, there are common steps to prepare.

````{grid} 1 1 1 3
:class-container: text-center
:gutter: 3

```{grid-item-card}
:class-header: bg-light

Step 1: Choices
^^^
The first step is to make some important choices, which will depend on the characteristic of the data, the project that produced it and its most likely use.
```

```{grid-item-card}
:class-header: bg-light

Step 2: Metadata
^^^
Metadata includes any information on the data itself. In a published record the metadata is usually available as a record abstract and inside the files (if using a self-describing format such as netCDF) or by auxiliary metadata files.
Ideally all this combined information should allow someone to reproduce the data from scratch (see [Provenance](../concepts/provenance)).
```

```{grid-item-card}
:class-header: bg-light

Step 3: Formatting files
^^^
Files should be well formatted to enhance their accessibility and usability.
```
````

`````{tab-set}
````{tab-item} Choices    
   :class-container: px-100 
**What** 

It's not usual or a good thing to publish all the data produced in a research project. It's important to identify what data is useful or required, considered other limitations like storage availability. Here are some considerations that can help with the choice.
1. Provide the information needed to interpret, reuse and reproduce the results. This is what journal publishers usually require, most of them provides [guidelines and examples](journals) of which data should be shared.
 
2. If the output is big, publish only a subset. If methods are well described, the software used is easily available, then publishing only the subset of data that underlines a publication is sufficient. For example, the post-processed output is sufficient for a model simulation. However, the model version and configuration used, the input data and model source code should be clearly documented.
 
3. Consider the strengths and limitations of the data, the way it was produced can limit what it should be used for. Model output is a good example of this, the way physical processes are parametrised, the resolution, the input data and other model components determine what the output data should or shouldn't be used for.

4. The data required for publication might be a small part of the overall output. It often happens with model output that a researcher only uses a small subset of variables, but others could be useful to other projects. If it is viable these can be added to the publication, but when resources to publish are scarce, providing information on their existence and on how to access them, may be enough. This should include details on license, possible use restrictions and details on how to create accounts with other institutions if necessary.

**Where**

There are different options to publish climate data, the most suitable for a research project will depend largely on the institution the researcher works for. This is explained in depth in the [next page](publish-options). It is worth remembering that while there should always be **only one DOI** per dataset, it is possible to create a metadata-only record pointing to the official DOI in other data portals to give more visibility to the data.
 
**Licence**

This is often left last and in most cases this is not an issue, however, it is important to know **from the start** of the research what are the *licensing terms of the data used as input* and, if the rules around licensing potentially imposed by the employer, the project itself and funding bodies. Big collaborative projects, like CMIP6, usually have their set of rules around licensing.
[Licenses](../concepts/license) are covered extensively in the concepts part of this book.
It is also worth to consider adding **term of use** and a **disclaimer** to avoid the data being misused accidentally.

**Version** 

Often researchers think they don't need a version for a dataset as they are not planning to publish a second version. However, it is common to do mistakes when publishing data, no matter how small the issue the result is often having to publish an updated version as a DOI is a persistent identifier and changes to the underlying files are not permitted. This is why it is always recommended to have a version. [Versioning](../tech/versioning) is covered in the technical tips part of this book. 

**Authors and collaborators**

Like journal manuscripts, datasets (and software) have an authorship list and collaborators. As for a paper, only people who contributed to the dataset (the data not the research project itself) should be listed as authors and, where appropriate, people who helped with the publishing process itself, for example formatting the data, as [collaborators](../tech/contributors). See also the [authorship page](../concepts/authorship) in concepts. 
````

````{tab-item} Metadata

**Dataset webpage**

The dataset page on the data portal provides the first data information for a prospective user. While there are differences among how this information is displayed, most of the elements are common to all portals.

A page will show a **title** and an **abstract**, it is important for both to be written considering an end user point of view. What would a user look for when considering using a dataset? What kind of information is essential for the data to be usable? Which additional information would make its use easier?
It's important to consider how the search engine of the portal works and how it displays results. Choosing relevant [keywords](../tech/keywords) and using terms from [controlled vocabularies](../concepts/controlled-vocab) helps. Words in the title are also prioritised by search engines and shown as part of the results list, so the [title should be as descriptive](../tech/title) as possible.
The abstract should use plain language and not assumed expertise of the field on a user side. For the same reason it is important to give the context in which the data was produced and highlight its appropriate uses. If there is a high risk for the data to be misused, then a disclaimer explaining the data limitations should be added too. While it’s important to share technical details to use the data correctly, it's worth considering adding this information in a separate file if it is extensive. We provide an [annoted example of a readme file](../tech/tech-readme) which show what kind of information should be considered. Data portals often have options to add related links, this is an easy way to provide as much relevant information as possible.

**Self-describing files**
Most of the file formats commonly used in climate are self-describing. An example are the attributes in a netCDF file. It is important to use these as much as possible to give a precise and correct definition of the data itself following available conventions. Using the self-describing properties of a file has two important advantages: it keeps important information with the data itself, and these files attributes are used by discipline software to simplify data analysis.
Publishers that deal regularly with climate data usually require at least for the [CF](../concepts/cf-conventions) and/or [ACDD](../concepts/acdd-conventions) conventions to be followed, however it is always worth applying them when possible even if they are not required for publication.

```{note}
Please note we cover CF conventions application and potential issues when they are used incorrectly in the [technical pages](../tech/conventions).
```


**Auxiliary files**

These could be any kind of text, tabular files or other formats like markup (xml, html, json, md etc.) that add information on the data. These could also be actual data files, for example the ancillary files used to run a model simulation. 
````

````{tab-item} Formatting files

**Files organisation**

The way files are organised in folders, their names and sizes should consider both how the files will be distributed and how they will be used. For example, the protocol used to download the files might have a maximum size allowed, likewise having to list a lot of small files it's inefficient when loading an html page. Names also should be descriptive enough that a file can be recognised easily after has been downloaded as being part of a specific dataset. We covered [files organisation and naming](../tech/drs-names) in the technical pages of this book, however, it is important to check the publisher instructions in this regard, or, if none are available online, contacting them about it as early as possible in the publishing process.  

**Conventions**

It is important to use [conventions](../concepts/conventions) and [controlled vocabularies](../concepts/controlled-vocab) whenever possible, both official ones, like CF conventions for file attributes, and others which are not a requirement but have become common practice in the climate community (e.g. CMIP variable names). As some of these conventions also apply to folder and file names, it is important to be consistent and use the same terms in the files, names and descriptions. 

````
````` 
