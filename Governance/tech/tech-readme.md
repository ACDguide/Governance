# Dataset readme file template

A good readme file attached to your published data is a useful tool for a potential user. If they have found the data online by downloading the readme file they can keep the data description and publications details together with the data. If they are using the data directly on the server where the data is stored, then they can get the information on the dataset without having to go online.

More importantly the data description shown on online repository is limited in size and a readme file is useful to add more technical details, direcotry structure and other information that you might have to leave out of the main abstract.

Readme template and example
When you are publishing on NCI we provide a Readme file template in the working directory we create for each dataset. here I am using a real readme file from a record we recently published to illustrate the template structure. This particular readme file is quite long as there are a lot of technical details, so it provides a good example to show the kind of information you can include. However, if your dataset is less complex is likely your readme file will be a lot shorter than this.

<Dataset title and version>

High-Resolution Modelling of Extreme Storms over the East Coast of Australia v1.0
 <Abstract usually the same as published record>

This dataset includes data of 11 extreme East Coast Lows simulated using a multi-physics (5), multi-resolution (3) approach for 4 different boundary conditions, leading to a total of 660 simulations. All simulations were performed using the Weather Research and Forecasting (WRF v3.6) regional model using a triple nesting approach with different domain sizes.
The outer domain corresponds to the CORDEX (Coordinated Regional Climate Downscaling Experiment) Australasia domain and is discretized using a 24-km horizontal grid spacing.
ECMWF ERA Interim (ERAI) reanalysis are use to initialize and drive the model for present climate simulations. For future climate simulations, the Pseudo Global Warming (PGW) approach is used. In this case, initial and boundary conditions are built by adding the climate change signal obtained from a global climate multi-model ensemble from the CMIP5.
We selected a total of eleven events featuring an extreme east coast low over the eastern coast of Australia. Events were selected based on their impacts around the Sydney area and the selection includes some of the most iconic events in recent times such as the "Pasha Bulker" (June 2007) and the June 2016 storms. All events were simulated for a total of 8 days, starting about 4 days before the storm peaked near the Sydney's area. A full list of events dates is given below. 
<list of relevant elements of the data as simulations,  data sources etc.>

Events:
2007-06-04 to 2007-06-12
2007-06-13 to 2007-06-21
2007-06-22 to 2007-06-30
2001-07-23 to 2001-07-31
2005-03-18 to 2005-03-26
2008-09-02 to 2008-9-10
2015-04-18 to 2015-04-26
2008-08-18 to 2008-08-26
2013-02-17 to 2013-02-25
2016-06-01 to 2016-06-09
2006-09-03 to 2006-09-11

Boundary conditions:
    HIST - (ERAI) reanalysis is used as lateral and surface (SST) boundary conditions for present climate simulations
    HIST-BRAN - (ERAI) reanalysis is used as lateral boundary conditions and BRAN for surface (SST), for present climate simulations
        FUT - initial and boundary conditions are built by adding the climate change signal from the CMIP5 RCP8.5 scenario climate multi-model ensemble to ERAI.
        FUT-THERMO - initial and boundary conditions are built by adding the climate change signal from the CMIP5 climate multi-model ensemble to ERAI, but only to thermodynamical variables (temperature and humidity) 
Physics:
There is one control run (CTL) and four perturbed physics members that include modifications in the cumulus (CU), the surface and planetary boundary layer (PBL), the radiation (RAD) and the microphysics (MPS) schemes. Members are denoted according to the physical scheme that is being changed compared to the CTL run. 
<extra information if necessary as more details on technical aspects, sources etc.> 

Table summary for physics
Name           |   CTL     |   CU      |   PBL     |   RAD    |  MPS
--------------------------------------------------------------------------
cumulus        | BMJ (2)   | KF (1)    | BMJ (2)   | BMJ (2)  | BMJ (2)
S/PBL          | YSU (1)   | YSU (1)   | MYJ (2)   | YSU (1)  | YSU (1)
shortwave rad. | RRTM (2)  | RRTM (2)  | RRTM (2)  | CAM (3)  | RRTM (2)
longwave rad.  | Dudhia (1)| Dudhia (1)| Dudhia (1)| CAM (3)  | Dudhia (1)
microphysics   | WSM6 (6)  | WSM6 (6)  | WSM6 (6)  | WSM6 (6) | Thomp. (8)
Numbers after each of the schemes denote the code used in the WRF namelist.
MYJ [9]; YSU [8]; KF [12, 11]; BMJ [1, 9, 10]; WSM6 [14]; Dudhia [6], RRTM
[15]; CAM [4].
<variables list> 

 The final data product is the post-processing files of all simulations made following CORDEX standards.
Names and units of the variables that are available after post-processing. The frequency and the level is also included. Pressure levels are 200, 500, 700, 850 and 925 hPa.
Surface level variables at 1 hr frequency:
   prm - precipitation rate (mm)
2m surface variables at 1 hr frequency:
   tas - temperature (K)
Surface level variables at 3 hrs frequency:
   psl - mean sea level pressure (hPa)
Near-surface level variables at 3 hrs frequency:
   cape2d - Convective Available Potential Energy - CAPE (J kg-1)
   tpw - total precipitable water (mm)
2m surface variables at 3 hrs frequency:
   hus - specic humidity (%) 
   hurs relative humidity (%)
10m surface variables at 3 hrs frequency:
   uas - zonal wind (m s-1) 
   vas - meridional wind (m s-1)
Pressure level variables at 6 hrs frequency:
   ta - temperature (K)
   ua - zonal wind (m s-1)
   va - meridional wind (m s-1)
   wa - vertical wind (m s-1)
   zg - gepotential height (m)
   hus - specic humidity (kg kg-1)
<Dataset creator, grants if relevant, CLEX research program or other project this dataset is an output of> 

This dataset was created by Dr Alejandro Di Luca as part of the Australian Research Council (ARC) Discovery Early Career Researcher Award (DECRA) funded project (DE170101191) and is part of the Centre of Excellence for Climate Extremes (CLEX) Extreme Rainfall research program.
<where to find the data online and how the data is organised on the server>

The data is available online on the NCI TDS server:
  https://dapds00.nci.org.au/thredds/catalogs/ks32/CLEX/HiRes-MESECA/HiRes-MESECA.html
and for NCI users in the ks32 project.
File organisation:
  /g/data/ks32/CLEX_Data/HiRes-MESECA/v1-0/<resolution>/<event>/<boundary conditions>/<physics>/<frequency>/<variable>/<files>
where
    <resolution> is WRF24, WRF8 and WRF2 for horizontal grid resolution of 24 km, 8 km and 2 km, respectively 
    <event> is the starting date of each event
    <boundary conditions> are FUT, FUT-THERMO, HIST and HIST-BRAN
    <physics> are CONTROL, CU, MPS, PBL and RAD 
    <frequency> are 6hr, 3hr, 1hr
 
filenames:
   <variable>_HiRes-MESECA_UNSW-WRF360-i1_<resolution>_<event>_<boundary conditions>_<physics>_<frequency>_v1-0.nc
Example: va200_HiRes-MESECA_UNSW-WRF360-i1_WRF2_2001-07-23_FUT_CTL_6hr_v1-0.nc
 < if there is more than one author and/or collaborators list the names and their roles in regard to the data>

Author:
 · Alejandro Di Luca: designed and performed calculations to generate historical and pseudo-global warming boundary conditions; conceived, designed and performed all simulations; coded and run postprocessing scripts.
Contributors:
·        Daniel Argueso (d.argueso@uib.es): designed and performed calculations to generate historical and pseudo-global warming boundary conditions; coded postprocessing scripts.
·        Nicolas Jourdain (nicolas.jourdain@univ-grenoble-alpes.fr): designed and performed calculations to generate pseudo-global warming boundary conditions.
·        Jason Evans (jason.evans@unsw.edu.au): installed and setup the model in the NCI supercomputer, helped on the design and performance of simulations.
<Main contact, if relevant specify a contact for scientific questions and one for file access>

Contact: di_luca.alejandro@uqam.ca for any question on the dataset content and provenance
         paola.petrelli@utas.edu.au for questions or issues with file accessibility
<Dataset citation, this should always include the dataset doi> 

Citation: 
    Di Luca, Alejandro, Argueso, D., Jourdain, N., Evans, J., 2021. High-Resolution Modelling of Extreme Storms over the East Coast of Australia v1.0. NCI National Research Data Collection, doi:10.25914/604eb7628b4e7
Other information you can include which was not present in this particular example are

References list, if you are citing other sources in the description
Associated papers for publications that are based on the dataset

