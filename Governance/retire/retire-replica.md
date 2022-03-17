# Retiring replicated data

Replicated data is usually retired to prioritise storage usage, occasionally because the data is flawed.

If the data contains a serious error you might want to block access to it as early as possible, as for published data. It might be useful to also quarantine the data, so remove access immediately but not deleting or archiving the data yet.
This is for reproducibility reasons, in particular if the dataset is complicated to re-download. However, as you are not the primary publisher it should generally be ok to remove the data entirely in a short time.

If the data needs to be retired to prioritise storage usage, then it is more complicated.
This is because it is hard in the first place to choose which data, or data subset, to retire, as this is based on your community needs.


## How to assess data usage

Assessing data usage is probably the hardest part of the process. Unless the data can be accessed only in one way, for example for published data that has to be downloaded, is really hard to find a reliable measure of active data usage.
In most cases you will have to use a combination of the methods which are available.
Some methods are automated{{{any better word??}}}, where you use any available statistics automatically saved by the data server or filesystem. These can be useful when managing a big dataset where you have set rules from the start, so that ongoing retirement of data subsets are anticipated and part of the regular management.
Even if you have a reliable automatic measure of data access it is always a good idea to consult the community. Automated methods can only record actual usage, to make an inform decision you also need to assess future and other potential usage. It is also important to have an idea of how the data is used, if an obscure variable is needed to produce a dataset that is widely used by the community, decide to retire it because there is only one person using it is not a good idea.

### automated methods
* Checking latest access time (`atime`) of the files (using the `stat` command) to see when a file was last accessed. Note that many operations can affect `atime` so it's important to do this before moving the data anywhere. This is only reliable if there are not automated processes that alter `atime` when running, for example a regular scan of the filesystem run by the system administrator. This can only tell you when a file was last accessed not how many users are accessing it. 
* Project user number: where users need to sign up to use the data (as for NCI project) you can easily get an idea of users' number and distribution. A limit of this is that it doesn't tell you who is actively using the data or which subset of the data is being used.
* Database queries: this can be used of course only if the data can be queried or accessed via a tool and this tool keeps logs of the queries. It is still imprecise as a user might be querying some data but not necessarily using it.
* Online downloads: usually data servers keep tracks of downloads of online data, as well as views. If the data is on Zenodo these stats are accessible to anyone, in other cases you might have to ask the data server administrators to collect them for you, if they don't do that automatically.
* ...???

### community feedback
* E-mail communication: this is possible where your community is well defined, so if users need to sign up to a group/project or if there are well defined community of potential users. For example, if the data is on NCI you can use my.nci.org.au to contact projects' users. This might be sufficient when you have already identified a likely candidate.
* Survey: this can be useful when you need to evaluate several datasets at one time or work out which subset of a a big dataset could be retired.
* ...??? 

### Suggested workflow

1. Using one or more automated methods to collect statistics on actual data usage.
2. Announce to users with data access the anticipated retirement of the dataset. If the data appears to be unused, move to a "quarantine" area nearby where users may still find the data and notify the data managers that it is still required.
3. If no objection is heard, the data can be staged for deletion. On the other hand if objection is heard, then a dialogue must be started with the affected users to identify an alternative support mechanism for the dataset.
4. After some agreed period, the data can be removed from the filesystem.


{{{ Should we cover or at least say something about really complicated cases? as for CMIP6 currently, I feel that we are not yet saying much on 
{{{The following is a list of topics I feel we should also cover here but I'm not sure how to integrate them:
1) CMIP like cases where the strategy should be a adopting a "continuous retirement", I mentioned that in the principles but maybe should be expanded there or here
2) having to move data on tape, so you're not fully retiring the data and you're not archiving it either. As for BARRA, data is on tape but probably not in complicated tarballs still structured in such a way is accessible "relatively" easily. It would cover the option where you are running out of storage but the data is still of use. So you can split it into priority data still on disk and less commonly used data on tape.
