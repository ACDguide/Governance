# Descriptive title

It is important to have a good title for your new data or code for publication. As you probably carefully choose a title for your papers, you should also try to put some effort in creating a good title for other research outputs. The title will be in any reference to your data or code.  While, depending on the repository you are using to publish, you can potentially change the title, even after a record has been published, it is important to get it right and be as descriptive as possible.

Also, most people querying a repository will skim quickly through the list of returned records. All they will see initially is the title and the start of the description. And finally, any word in the title is used as a keyword by free text search engine.

## What to include
Keeping in mind that the title words are used as keywords, a good rule of thumb is to include the sort of information that a potential user might choose for a search. The most important are probably the kind of data, the region, temporal coverage and frequency of the data. 
Where it is relevant the source of the data should also be included, for example if this is a dataset derived from CMIP6, it might be interesting for anyone searching for CMIP6 data. If it is a model output, the name and version of the model would give a lot of useful information to understand the potential use of the data.
If publishing data or code underlining a paper publication usually this is clearly stated in the title. Similarly, it can be useful to mention the project associated to the research output, as giving the context in which the data or code was created can also clarify potential future use.

If publishing code, it is important to include its scope and how it can be run, so including the language on which is based and potentially a specific environment for which it was created.

## Data example
"Weather Research and Forecasting (v3.6) model outputs from 2 km Kuala Lumpur urban climate experiments"

In the example above the author tried to include:

* the model name and version - Weather Research and Forecasting (v3.6)
* the kind of data - model outputs
* simulation resolution - from 2 km
* spatial domain - Kuala Lumpur
* subject - urban climate
* that there is more than 1 experiment - experiments

<br>
```{note}
Having used the full model's name rather than an acronym clarified to any user not familiar with WRF that these are weather forecast related experiments.
```

## Code example
"CleF - Climate Finder a python based command line tool to query ESGF datasets hosted at NCI"

In the example above the author tried to include:

* the code acronym and full name: CleF - Climate Finder
* that it is python based - python
* that it is executed as a command line - command line tool
* what it does, including the data to which is applied: to query ESGF datasets
* the specific environment for which it was built: hosted at NCI
