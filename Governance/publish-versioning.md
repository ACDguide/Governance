# Versioning

Versioning is the process of creating and managing multiple releases, each labelled by a version, of a research output, such as a dataset or code. Applying versions consistently and clearly is really important, as different releases can have fairly different characteristics and their applications can produce very different results. There are several discussion groups and documents dedicated to the topic of versioning, here we are trying to cover only the essential aspects. 

## Code versioning
Versions are really important to identify your code, even if you are using already a version control system. Even if you are not planning new releases it’s fairly common to have updates with code. Consider following the [Semantic Versioning convention](https://semver.org/), this scheme uses a 3 part version number,

     MAJOR.MINOR.PATCH  as in v1.3.0

* MAJOR changes when the updates will break previous behaviour, use “0” to indicate a code still under development
* MINOR changes when adding new functionality in a backwards compatible manner
* PATCH number when you make backwards compatible bug fixes.

If you are using GitHub, produce a release before publishing. While a commit url is a persistent indicator of a specific code snapshot, it is not easy to share, and commits message usually refer only to the last step.

Most of all it is important to be consistent and versions should always progress from lower to higher.

## Dataset versioning
As for code even if you are not planning any new version of the dataset, you might change idea or need to extend or correct the data in the future.

Conventions around data versioning are still been developed. The ARDC provides some [guidance](https://ardc.edu.au/resources/working-with-data/data-versioning/). 

### Completed dataset
Here are some suggestions to work a versioning strategy for a “stable” dataset

Any change in the actual data should be accompanied by a new version.
Changes to the metadata do not need a new version.
Most often numbers or time stamps are used to identify versions, whichever approach you choose, it is important to be consistent. It is impossible for a user to work out which version is the latest if two versions are called v2.0 and v2020. 

### Continuous dataset
Datasets which are continuously updated require particular attention. As a starting point you should apply the same versioning strategy used for a “stable” dataset. However, you also need to consider the following:

The documentation should report how the dataset is updated and how frequently.
It is better to add new files, if possible, rather than updating existing files.
It is even more important to have a versioning strategy to distinguish between the constant change to the data, allowed as part of the same version, and what circumstances will warrant the creation of a new version.
When the way the data is produced changes, then there should be a new version, even if the older data in the timeseries is not affected by the change in methodology.
As a DOI should always refer to exactly the same object there is not consensus on how to treat continuous data. Some of the common strategies are:

Publishing the data at regular time intervals, i.e. every year. This is done at times delaying the data release, so the data is always covered by one DOI or updating the data continuously and leaving gaps in the DOI coverage. In both cases each new DOI will be reflected in a new version
Publishing the DOI and updating the data continuously until a change in data production warrant the creation of a new version. Users are then required to add a timestamp indicating when the data was accessed in the dataset citation.
````
```{admonition} Know your publishing tool
Depending on the data portal you will be using to publish, a version update might be imposed when you make changes. For example, if you are using Zenodo adding or removing files will force a new version to be created.
```
````
