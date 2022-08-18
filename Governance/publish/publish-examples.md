# Best Practice Published Data Records

The climate community is in better position with respect to best practice data management than many other groups due to the self-describing data format of [netCDF](https://www.unidata.ucar.edu/software/netcdf/) and community modelling projects such as [CMIP](https://www.wcrp-climate.org/wgcm-cmip)/[CORDEX]( https://cordex.org/)/[Obs4MIPS]( https://pcmdi.github.io/obs4MIPs/) enforcing a strict standard. There are lots of climate-tools in wide use across the community that make use of this fact, including modifying the history attribute to document what was done to the data.

**What does best practice look like?** Certainly, it *does* look like including all metadata, ensuring data is [FAIR](https://www.go-fair.org/fair-principles/)/[FAIRER](https://acdguide.github.io/Governance/concepts/fairer-principles.html) [^1], documenting data processing and publishing that as well, undertaking QA/QC and documenting the process.

It is near impossible to get all this right and even with strict standards like CMIP/CORDEX we still find mistakes in the metadata due to the complexity of the standards. We will never get this perfect but aim for a best effort and as our tooling (software/workflows) improve over time so will our compliance.

How do we walk the line between showing people what their data should look like, and not putting them off from making any effort at all by suggesting they have to get it perfect? 

For examples of good practice, we suggest looking at the following:

- Bureau of Meteorology (2021): Seasonal Prediction ACCESS-S2 Reanalysis (1981-2018). NCI http://doi.org/10.25914/60627ad8878e2 

- Bureau of Meteorology (2021): Australian Gridded Climate Data (AGCD) v2. NCI http://doi.org/10.25914/6009600786063 

- Dix, Martin; Bi, Dave; Dobrohotoff, Peter; et. al (2019): ACCESS-CM2 model output prepared for CMIP6 under 'ScenarioMIP'. v2. CSIRO. Service Collection. http://hdl.handle.net/102.100.100/422393?index=1 

- Durrant, Thomas; Hemer, Mark; Smith, Grant; Trenham, Claire; Greenslade, Diana (2019): CAWCR Wave Hindcast - Aggregated Collection. v5. CSIRO. Service Collection. http://hdl.handle.net/102.100.100/137152?index=1

- Earth System Grid Federation (ESGF) Australian CMIP6-era Datasets (2021)
NCI. http://doi.org/10.25914/5e6acd0492b39


[^1]: Trenham, Claire; Steer, Adam. The Good Data Manifesto. In: Daly, Angela; Devitt, Kate; Mann, Monique, editor/s. Good Data. Amsterdam: Institute of Network Cultures (INC) Publications; 2019. 37-53. https://networkcultures.org/blog/publication/tod-29-good-data/.
