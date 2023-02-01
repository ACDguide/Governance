# General principles of data retirement

It may be necessary to retire a dataset for several reasons:

- the data is seriously flawed and access to it needs to be removed
- the data is not used by our community anymore
- need to prioritise how storage is being used

In any case we must proceed carefully and make sure we have considered all the implications of removing the data. As mentioned in the introduction, the most important factor is if the data is published.

## DOI persistence requirements

**If data is published with a DOI** (or equivalent persistent identifier), there is an obligation to maintain the landing page of that DOI indefinitely - this persistence of URLs is what data publishers like Zenodo, NCI and the CSIRO Data Access Portal provide. 

Digital Object Identifiers (DOIs) are minted so that data can be found reliably from a single source. The landing page of the persistent URL associated with the DOI should be a metadata page describing the dataset, and if public, providing access to the data.

If data is retracted or replaced with an updated version, the DOI associated with the original version needs to still resolve. It is possible, in cases of data error, to add a note on the metadata landing page indicating that the dataset has been withdrawn.

It is not permissible to simply remove a DOI, though it may be necessary to redirect to a ["tombstone page"](https://support.datacite.org/docs/tombstone-pages) which resolves to a page that explicitly states that the dataset is no longer here.

Every new version of a dataset (e.g. due to changes in the data) requires a new DOI.

## Data usage

Sometimes a **dataset needs to be retired** (removed from a shared filesystem, from which it has not been published) because it is no longer used, for example:
- the researchers who used the dataset are no longer working with it, 
- the researchers who created data have left the field, or 
- the dataset has become obsolete due to newer datasets which support the same research. 

This is a difficult situation to navigate because it can be hard to identify who may still be using the data on a filesystem, and whose workflows would be affected if the data is removed. Nevertheless, it is important to assess the use of the dataset and the value of the cost of ongoing storage.

## Storage availability

For very large datasets, it may not be possible to store a copy of all versions of the data, and the data may have to be replaced.

When a project that funded creation of a dataset ends, it is often necessary to have the published data associated with the project, however, no **ongoing funding** from the project is available to maintain the data or the storage hosting it. Currently the cost of ongoing hosting of published datasets is borne by the research institutions, however it is hoped that in the future research grants and funded projects will consider storage costs during and after the project.
We have not yet dealt with the situation of a dataset needing to be retired because no funding was available to support its ongoing hosting, but it is a consideration we may need to bear in mind.

## Data archiving

When practicable to do so, retired datasets should be archived to a deep store, which may be slow to access and not appropriate for web serving, nevertheless, it enables, if necessary, analyses conducted on the retired data to be repeated, that is, reproducible science.

Most data facilities (including NCI and CSIRO) have tape archives where data can be backed up or stored when it is no longer readily required. However, there is still some cost associated with this storage, and it is not infinite in scale, so it is not always an appropriate solution, but it should be used when viable to do so.

## Communication

Keeping the community informed and updated is an important part of the retirement process.
Ideally the retirement process should be planned and advertised before there is any need to retire the data.
A retirement plan can be a dedicated errata service or simply a retirement policy.
Many publishers do not offer an errata service (see links in Further Information), preferring instead to keep all data. In this case, **an errata statement explaining what change was made needs to be issued and made available on the DOI landing page of the dataset**. [Here is an example](https://research.jcu.edu.au/data/published/1507eae78675ccfb3843eb9d004cbb96/) of a data retraction.
An example of errata service is the [Earth System Documentation errata service](https://errata.es-doc.org/static/index.html). It provides a record of all known issues and where appropriate, data withdrawal and republication. 

It would be cumbersome to produce a plan for each dataset managed. However, as most datasets particularly if they are replicas, can follow the same procedure it is beneficial to have at least a document explaining when and how the data might be retired without going into specifics. An example of this is in the policies for the [CLEX collection on Zenodo](https://zenodo.org/communities/arc-coe-clex-data/about/#retention_policy).

<!-- COMMENT!!!! once we have a similar policy for the ACS reference collection we could maybe use that as an example instead !!! -->

A retirement plan should include:
- in which circumstances the data might be retired
- how and if the data will still be available elsewhere or by request
- a timeline of the changes, including enough time for comments to be dealt with 

It is much easier to make clear from the start what responsibility you assume when providing a dataset for others to use, rather than dealing with disappointed users down the track.

Similarly, once you start the retirement process you should:
* Inform the community as widely as possible, and at regular intervals via email, if possible.
* If the data or metadata is available online, add a highly visible notice of the impending retirement.
* Have a period of quarantine when the data is no longer accessible but hasn't been deleted or archived yet. There are always users who will notice the data is gone just when trying to use it, no matter how many times you try to inform them.
* Make sure that you include information on alternative data sources and explain the reasons for the retirement.

In some cases, it is appropriate to consult with the community before making a final decision for data retirement. This is usually the case when dealing with replicated data and shortage of storage and it will be covered in that use case section. 

