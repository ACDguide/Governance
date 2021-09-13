## Controlled vocabularies

A [controlled vocabulary](https://www.ands.org.au/guides/vocabularies-and-research-data) is an agreed list of terms definitions used to provide a unique label to a concept. Controlled vocabularies are usually discipline related; their main aim is to facilitate sharing of data in the same community. For this reason, it is important that the community participate in the development of the vocabulary and agrees to its adoption for this to be useful.

In some case vocabularies have been created in relation to a specific project, and then more widely adopted. As an example, since CMIP is an intercomparison project with modelling groups participating from across the world, it was essential to its success to define and use controlled vocabularies. [CMIP6 controlled vocabularies](https://github.com/WCRP-CMIP/CMIP6_CVs) cover many different aspects: experiments, variables, realms, models, sub-projects, frequency, resolution and grid labels. Their definition and labels for variables, frequency and realms are often adopted by other climate data producers.

Another example of controlled vocabulary is the [CF conventions standard_name table](https://cfconventions.org/standard-names.html), anyone can contribute by proposing a definition for variable which are not yet covered.

### Keywords
Controlled vocabularies also provide keywords to use when publishing data. Keywords are a powerful instrument when used properly. They can greatly increase the discoverability of a dataset, which is why it is one of the few highly recommended attributes in the [ACDD conventions](http://climate-cms.wikis.unsw.edu.au/Conventions). Unfortunately, there is not yet an agreed controlled vocabulary to be used specifically for climate science. Lots of climate terms are however covered by the [Global Change Master Directory Keywords](https://earthdata.nasa.gov/earth-observation-data/find-data/idn/gcmd-keywords), maintained by NASA.

There are few categories you should try to cover when assigning keywords:

* dataset acronym: if your data is strictly related to another dataset, or your code is applied to a specific dataset
* model acronym and version: as for datasets if you generated the data using a model
* project acronym: if your dataset and or code relates to a specific project 
* programming language:  you should add this to your code records and be as specific as possible, for example use python3, rather than just python
* data type: observation, model output, etc.
* realm or discipline: like ocean, land and/or physical ocanography, climate science etc. For the disciplines you can use the [Fields of Research codes](http://climate-cms.wikis.unsw.edu.au/Field_of_Research_codes) from the Bureau of statistics
* variable names: if you have many just list the more relevant
* spatiotemporal characteristic of the data: frequency, resolution, region covered
Every time you define a keyword you should favour terms provided in a vocabulary, the GCMD keywords for example will cover most of the categories listed above. If you are using a speciifc name as for datasets, models and projects, then use the official acronyms and specify the versions whenever possible.

Also remember that if a portal has a free text search any word in your title will be also used as a keyword, which is why it is useful to have a [descriptive title](http://climate-cms.wikis.unsw.edu.au/Descriptive_title) for your dataset or code.

### Research Vocabulary Australia

ARDC manage a controlled vocabulary service [Research Vocabulary Australia](https://vocabs.ardc.edu.au/) (RVA) to list vocabularies used by Australian research community. As well as making it easier to find controlled vocabularies, RVA also allows research organisation to contribute and publish new vocabularies. 
