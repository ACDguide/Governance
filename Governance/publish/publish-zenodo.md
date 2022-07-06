# Publishing with Zenodo

Zenodo is an initiative funded by CERN that allows anyone to share their research outputs and mint a DOI for them. Zenodo is funded for at least the next 20 years and so it offers a good long-term solution, as well as being widely used internationally.

## How to publish
Publishing a dataset is easy and quick as long as the data is reasonably organised and has a detailed provenance.

* Create a Zenodo account, ORCID can be used to login.
* Read and follow the Zenodo [policy](https://about.zenodo.org/policies/) and [terms of use](https://about.zenodo.org/terms/).
* Create a Zenodo record for the dataset, uploading the relevant files. CLEX has prepared a [step-by-step guide](http://climate-cms.wikis.unsw.edu.au/images/1/10/Publish_your_data.pdf) on how to do this, which also cover the kind of information you should include.

## Useful tips 

* A dataset can have several authors, they all should agree to the dataset publication and to list the record on Zenodo. All authors should have made a significant contribution to the data.
* Make sure the files:
    * are following any relevant standards, if they are netcdf files they should follow both [CF](../concepts/cf-conventions) and [ACDD](../concepts/acdd-conventions.md) conventions.
    * have [descriptive names](../tech/filenames.md) and are organised in [directories](../tech/drs.md) in a way that facilitate their access and use;
    * have a [version](versioning-data) and a [license](../concepts/license-data.md) assigned.
* Use [keywords and controlled vocabularies](../concepts/controlled-vocab.md) in the metadata to increase discoverability.
* If the data has already been published elsewhere, a record on Zenodo can still be added to improve visibility. In such case use the existing DOI, **do not create a new DOI for the same data**. Instead of uploading the actual data files, a Readme file can be uploaded and links to the original records added for data download.
* Remember only datasets which are less than 50GB can be published. Exceptions are possible, see the relevant information in the [Zenodo's FAQs](https://help.zenodo.org)
* It's easier to zip the files and upload them as one file. An alternative if you have many files is to use the [Zenodo API](https://developers.zenodo.org).
* A community can be chosen if there is one that is relevant to the record. This will improve discoverability. The community administrators will receive a notification and either approve the record or contact the main author if they need extra information. Remember the data can be listed in more than one community. 
