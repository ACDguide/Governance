# Publishing options
Once the data is created and ready for publication, **where** can it be published? 

One of the main factors is what services are available, this is largely determined by the researcher's institution and/or organization.
Another important consideration is the kind of data, depending on format, size etc. using a public repository might be suitable and at time easier.
In some cases, depending on the dataset, using a public repository is suitable and often the easiest option. ori
On the other end of the scale, some data could be produced on purpouse or simply be suitable to contribute to a large-scale project that has its own publishing procedure established.
Here we are covering the most common use cases for our community.

::::{tab-set}
:::{tab-item} BoM 
Insert here pathways for BoM researchers...



:::

:::{tab-item} CSIRO 
Data, software and links to external data holdings (such as NCI) can be added to the [CSIRO Data Access Portal](https://data.csiro.au/) (DAP) by **CSIRO staff** only. More information on creating metadata records and uploading files to the CSIRO DAP can be found on the [DAP Help Guide](https://confluence.csiro.au/display/dap/Deposit+and+Manage+Data) (staff only access).

 CSIRO-affiliated data can be published in the DAP and the lead creator does not have to be CSIRO staff member.
:::

:::{tab-item} CLEX
We are looking here at CLEX as an example but as basically CLEX is only a collaboration project among universities, a lot of what applies here it is also usually applicable for anyone who works/studies in another university. Researchers working for a university have potentially more freedom in terms of where they can publish data. Unless they are working for a project which is covered by a data agreement and has specific licensing and/or data distribution requirements, the approach is to follow the FAIR principle and they are usually expected to share data openly.
Part of making data FAIR is to make it discoverable, so sharing data in a discipline specific collection is to be preferred when possible. This could be a collection of climate data, or of a related discipline, i.e., paleoclimate data, oceanographic data, etc. 
  
**CLEX Data Collection on NCI**
This is the best option if the data is in NetCDF format and could be useful for other researchers, as it will be part of a climate data collection. It is also the only option if the size of the data is substantial, in the order of hundreds of GB or more. NCI has more storage capacity than other repositories and services which are designed around the NetCDF format.
NCI requires the data to be documented and follow conventions, which will make the data easier to use. 

**Institutional repository**

This is adequate if the data is small and its reuse by others is unlikely. For example, data published only to reproduce the figures in a paper. While institutions offer some data curation, they usually will not check that the data is well described, consistent and user friendly, as they cannot be expert in every field. The data will get a DOI assigned but no added value. Institutional repositories might also have size restrictions. 
An institutional repository might not be able to publish big datasets effectively. 

**CLEX Data Collection on Zenodo**
For CLEX researchers, students and associates, the CMS team offers advice and can review a record, as well as add it to the [CLEX Data Collection community](https://zenodo.org/communities/arc-coe-clex-data/?page=1&size=20) to improve discoverability.
For more information on Zenodo see the generic options tab.
:::

:::{tab-item} Generalist repositories

Repositories like [Zenodo](https://zenodo.org), [Figshare](https://www.google.com/search?client=safari&rls=en&q=figshare&ie=UTF-8&oe=UTF-8), [Mendeley](https://www.data.mendeley.com) are public, generic data repositories. It is usually easy to create an account, add a data record and mint a DOI for it. These repositories also publish different kind of materials. This can be useful if publishing code together with data, for example code and data to produce a specific figure required to publish a paper. 
Another advantage is that these services are widely used and so you are more likely to reach an international audience.

However, as they are generalist repositories, there are no standards required or anyone checking the metadata. It is left to the researcher to make sure their data is as FAIR as possible. As the record won't be part of a discipline repository or collection, it is important to use keywords in an effective manner to make the data Findable. It is also important to have enough metadata and apply discipline standards and conventions to make the data Accessible, Interoperable and Reusable.

Finally, as for institutional repositories, the data size is limited to 50-100 GB and files can only be downloaded. 
We are covering [Zenodo](publish-zenodo.md) more in detail as it is available to anyone and the most used in our community. Figshare is not free but it might be available via an institutional account. Mendeley is free but lees used for climate data.
:::

:::{tab-item} Discipline repositories

In some cases, the data might be fit to be published to a specific data portal or as part of a larger initiative.
Of these we are covering only the ESGF case more closely, as it provides an example of a comprehensive publishing process. For the others refer to their websites for more information or there might be some relevant examples at the end of this guidelines.
Keep in mind that some of these options can be an extra distribution option for your data even if it is already published elsewhere.

[ESGF](https://esgf.llnl.gov) - the Earth System Grid Federation is a collaborative project responsible for the publication and distribution of climate model output as CMIP, CORDEX and other associated datasets. We are covering in detail the [procedure to publish CMIP and CORDEX data with ESGF](publish-esgf.md) (usually via NCI). Even if you are not contributing officially to one of these projects, the post-processing part of this procedure can still be applicable to generic ACCESS model output or "unofficial" CORDEX simulations. It also provides a good overview of what you should consider when publishing any kind of model output, in particular at a collaborative project level. 

IMOS

TERN

AURIN

Paeloclimate

Copernicus CDS/C3S
:::

::::
