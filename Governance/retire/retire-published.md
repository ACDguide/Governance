# Use case: published data
**If we publish data with a DOI** (or equivalent persistent identifier), we are obliged to maintain the landing page of that DOI indefinitely - this persistence of URLs is what data publishers like Zenodo, NCI and DAP provide. 
However, there are times when we need to delete the old data because it was seriously flawed and should not be used. In this case, **consideration must be given to the importance of reproducibility of science using the flawed dataset**.

If data is to be unpublished, we need to consider whether a copy of the old version can and should be archived on a tape store (e.g. NCI's MDSS) or if it is safe to delete the data. **In general, a copy of all published data should always be kept by the publisher, even if it contains errors**.


It is not permissible to simply remove a DOI, though it may be necessary to redirect to a "tombstone page" which resolves to a page that explicitly states that the dataset is no longer here.

Every new version of a dataset (e.g. due to changes in the data) requires a new DOI.

## Data archiving

When practicable to do so, retired datasets should be archived to a deep store, which may be slow to access and not appropriate for web serving, nevertheless it enables, if necessary, analyses conducted on the retired data to be repeated, that is, reproducible science.

Most data facilities (including NCI and CSIRO) have tape archives where data can be backed up or stored when it is no longer required. However, there is still some cost associated with this storage, and it is not infinite in scale, so it is not always an appropriate solution, but it should be used when viable to do so.

