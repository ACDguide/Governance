# Guidelines to manage the retirement of a dataset

Sometimes it becomes necessary to "retire" a dataset. This page covers some of the cases and considerations that come into play.

For the purposes of scientific reproducibility, in an ideal world we would never need to retire data. However, data centres are not infinite and thus we may find ourselves needing to remove data from a publication or filesystem.

## Scope of the guidelines

This page is intended to provide general guidance on
* data that has been superceded by a new version
* data that contains a serious error
* data associated with a project that is no longer active
* data that was never published but needs to be archived or replaced

The process may be similar in many cases, but it is important to give consideration to how others may be using a dataset before acting, as well as any maintenance obligations associated with having published the data.

### Index
* General principles of data retirement
* DOI persistence requirements
* Data archiving
* References and further information

## General principles of data retirement

It may be necessary to retire a dataset when a new version of the data becomes available.

The new version may be 
- as a result of updated processing code that produces more accurate data, 
- because of an error in the metadata associated with the previous version, or 
- because of an error in the data itself.

The first case defines the updated dataset as being a new *version* of the data (e.g. v1 -> v2) which would require a new DOI if published. The second case reflects what in software would be considered a *minor release* (e.g. v1.1), it will attract a new metadata record but not a new dataset version number or DOI. The final case may require a full retraction of the original data and metadata, moving any publication landing page to a "tombstone page" and archiving the data, with a new DOI being minted for the updated dataset.

**If we publish data with a DOI** (or equivalent persistent identifier), we are obliged to maintain the landing page of that DOI indefinitely - this persistence of URLs is what data publishers like Zenodo, NCI and DAP provide. However, there are times when we need to delete the old data because it was seriously flawed and should not be used. In this case, **consideration must be given to the importance of reproducibility of science using the flawed dataset**.

If data is to be unpublished, we need to consider whether a copy of the old version can and should be archived on a tape store (e.g. NCI's MDSS) or if it is safe to delete the data. **In general, a copy of all published data should always be kept by the publisher, even if it contains errors**.

For very large datasets, it may not be possible to store a copy of all versions of the data, and the data may have to be replaced. In this case, **an errata statement explaining what change was made needs to be issued, and made available on the DOI landing page of the dataset**. Many publishers do not offer an errata service (see links in Further Information), preferring instead to keep all data, but for very large scale climate simulation data, for example, the [Earth System Documentation errata service](https://errata.es-doc.org/static/index.html) provides a record of all known issues and where appropriate, data withdrawal and republication. For smaller scale data, [here is an example](https://research.jcu.edu.au/data/published/1507eae78675ccfb3843eb9d004cbb96/) of a data retraction.

When a project that funded creation of a dataset ends, it is often necessesary to have published data associated with the project, however, no **ongoing funding** from the project is available to maintain the data or the storage hosting it. Currently the cost of ongoing hosting of published datasets is borne by the research institutions, however it is hoped that in the future research grants and funded projects will give consideration to storage costs during and after the project.
We have not yet dealt with the situation of a dataset needing to be retired because no funding was available to support its ongoing hosting, but it is a consideration we may need to bear in mind.

Sometimes a **dataset needs to be retired** (removed from a shared filesystem, from which it has not been published) because it is no longer used, for example because 
- the researchers who used the dataset are no longer working with it, 
- the researchers who created data have left the field, or 
- the dataset has become obsolete due to newer datasets which support the same research. 

This is a difficult situation to navigate because it can be hard to identify who may still be using the data on a filesystem, and whose workflows would be affected if the data is removed. Nevertheless, it is important to assess effective use of a dataset and value of the cost of ongoing storage. A suggested workflow for this case might be:
1. Check the latest access time (`atime`) of the files (using the `stat` command) to see when a file was last accessed. Note that many operations can affect `atime` so it's important to do this before moving the data anywhere.
2. Announce to users with data access the anticipated retirement of the dataset. If the data appears to be unused, move to a "quarantine" area nearby where users may still find the data and notify the data managers that it is still required.
3. If no objection is heard, the data can be staged for deletion. On the other hand if objection is heard, then a dialogue must be started with the affected users to identify an alternative support mechanism for the dataset.
4. After some agreed period, the data can be removed from the filesystem.

The same process may be appropriate for removal of a previously published dataset, though usually a published dataset would be replaced with a new/corrected version, rather than simply removed.

## DOI persistence requirements

Digital Object Identifiers (DOIs) are minted so that data can be found reliably from a single source. The landing page of the persistent URL associated with the DOI should be a metadata page describing the dataset, and if public, providing access to the data.

If data is retracted or replaced with an updated version, the DOI associated with the original version needs to still resolve. It is possible, in cases of data error, to add a note on the metadata landing page indicating that the dataset has been withdrawn.

It is not permissible to simply remove a DOI, though it may be necessary to redirect to a "tombstone page" which resolves to a page that explicitly states that the dataset is no longer here.

Every new version of a dataset (e.g. due to changes in the data) requires a new DOI.

## Data archiving

When practicable to do so, retired datasets should be archived to a deep store, which may be slow to access and not appropriate for web serving, nevertheless it enables, if necessary, analyses conducted on the retired data to be repeated, that is, reproducible science.

Most data facilities (including NCI and CSIRO) have tape archives where data can be backed up or stored when it is no longer required. However, there is still some cost associated with this storage, and it is not infinite in scale, so it is not always an appopriate solution, but it should be used when viable to do so.

## Further information

[DataCite](https://support.datacite.org/docs/what-is-a-doi) provides the authoritative guidance on DOIs and associated processes.

Each data publisher should have a policy on how to manage data withdrawals. Some examples are provided here.

- [CSIRO DAP "Withdraw a Public Collection"](https://confluence.csiro.au/display/dap/Withdraw+a+Public+Collection) (visible to CSIRO staff only) retains data on the system but permits limiting visibility.
- NCI's policy is not known/not publicly available at this time.
- [Zenodo "Removal" policy](https://about.zenodo.org/policies/) views withdrawal as an "exceptional action" and serves a Tombstone page in the place of the original landing page.
- [Figshare](https://help.figshare.com/article/can-i-edit-or-delete-my-research-after-it-has-been-made-public) permits versioning but not deletion.
- [Dryad](https://datadryad.org/stash/faq) views data removal as an "exceptional action" which should only occur "if there are concerns over privacy or data ownership".
- The Australian Ocean Data Network does not have a public policy on data withdrawal but uses the same method as many other publishers of retaining all data but using versioning where required. They strongly discourage uploading data until the researcher is positive it is in its final state.
- [University of Reading (UK)](https://researchdata.reading.ac.uk/preservation_policy.html) withdraw data from public view but do not delete, and use versions. [Birkbeck (UK)](https://researchdata.bbk.ac.uk/policies.html#withdrawalpolicy) have a similar policy.

In all cases, the course of action if needing to remove a published dataset is to contact the data publishing host (NCI, CSIRO etc) and discuss how to proceed on their platform, as well as any errata requirements to populate the Tombstone page.