# Code repository for Mallett et al. (2021; The Cryosphere)

## Introduction

This repository contains all the code necessary for replication of Mallett et al. (2021).

*Mallett, Robbie DC, et al. "Faster decline and higher variability in the sea ice thickness of the marginal Arctic seas when accounting for dynamic snow cover." The Cryosphere 15.5 (2021): 2429-2450.*

## Overview of steps to reproduce the sea ice thickness data

- Download daily ice-type data, average to monthly and regrid

This data is downloaded at daily time resolution from the Copernicus Data Store using a python script. 
The downloader script is available in code/processors/Download_Ice_Type_Data.ipynb
This produces one giant folder with loads of files.
The next steps of the analysis are done using code/ice_type/cds_daily_to_monthly_and_regrid.ipynb
Here the files are dispatched to an individual folder structure with a folder for each month of each year
The daily files for each month are then stacked and averaged using the command line tool cdo, which is called from within the notebook. 
This is what the p=subprocess.Popen() call does. Spicy!
Finally all the monthly data for each year are aggregated into annual netcdf files using xarray. 

- Make monthly mW99 2002-2018

To make mW99 you first need to make W99. This is done using the quadratic coefficients from Warren et al., 1999 (J. Clim).
These coefficients are given in Warren_climatology.xlsx, and can be projected onto coordinates of your choosing using W99/W99_Gridder.ipynb
W99 is then saved as a pickle file (e.g. W99_361.p for the analysis in this paper)
Once you have the gridded W99 data, all you need to make mW99 is to combine it with the ice type data.
This is done in W99/mW99_maker.ipynb. Annual netcdf files of mW99 are made using xarray

- Download daily SnowModel-LG data and average to monthly

The SnowModel-LG data required to reproduce the findings and figures in this paper can be downloaded from https://doi.org/10.5067/27A0P5M6LZBI
You'll find 4x ~7 GB netcdf files. The original analysis for this paper was done using raw .gdat & .ctl files. There may be some references and allusions to these in the repo, but all analysis has now been redone from the raw .nc files for ease of replication.
Please note, the lon/lat EASE coordinates are not provided with the .nc files - these can be found in mask.nc within the repo.
When you've downloaded the SnowModel files, the first task is to convert them to monthly averages using SM_daily_to_monthly.ipynb.

- Download monthly radar freeboard data from CCI & AWI

First get as much data from CCI as possible:
Envisat data: https://catalogue.ceda.ac.uk/uuid/f4c34f4f0f1d4d0da06d771f6972f180
CryoSat2 data: https://catalogue.ceda.ac.uk/uuid/ff79d140824f42dd92b204b4f1e9e7c2
Now "top up" the CryoSat-2 data from the AWI ftp site, as the CCI data doesn't go quite up to 2018:
I use (from the command line) ``` ncftp ftp://ftp.awi.de/sea_ice/product/cryosat2/v2p3/ ```

- Download NESOSIM data

Download the files from here (only has up to 2015, which is all that was considered in the paper):
https://earth.gsfc.nasa.gov/cryo/data/nasa-eulerian-snow-sea-ice-model-nesosim
Process these into monthly mean files with Nesosim_monthly_processor.ipynb

- Calculate thickness components from the snow data sets and the radar freeboard data

This is done with code/processors/Calculate_thickness_components.ipynb and a bunch of helper functions from custom_tools that call the relevant data
This makes annual netcdf files with the SIT components (snow and RF) for each month.

## Overview of steps to reproduce the main figures

**Figure 1**: The regions of the Arctic Ocean are visualised using Fig_mask_map.ipynb

**Figure 2**: The drift-tracks and sampling of the NP drifting stations in the different regions are plotted in processors/Analyse_drift_tracks.ipynb

**Figures 3, 4 & 5** are made using SM_Climatology.ipynb

**Figure 6** is made using Regional_W99_vs_SMv2.ipynb (search for the function ```snow_contribution_timeseries_limited```)

**Figure 7** is made using the above notebook. Search for the function ```plot_radar_snow_correlations```

**Figure 8** is made using the above notebook - search for the function ```abs_var_bar``` (part a) and ```rel_var_bar``` (part b).

**Figure 9** As above: ```abs_var_summary``` and ```rel_var_summary```

**Figure 10** As above: search for the ```timeseries``` function.

**Figure 11** Same as above. Search ```abs_trends_summary``` (part a) and ```rel_trends_summary``` (part b).

## Overview of steps to reproduce the supplementary figures

**Figure S1**: Value of the propagation factor used to convert radar freeboard to ice freeboard, plotted as a function of snow density. This is made using Fig_linear_propagation.ipynb.

**Figure S2**: The number of valid, 25×25 km radar-freeboard grid cells in each region for each month. Made using Regional_W99_vs_SMv2.ipynb.

**Figure S3**: Difference in snow depth in SnowModel-LG when driven by ERA5 and Merra2 reanalysis data. Made using two notebooks: Compare_SM_reanalysis_difference1/2.ipynb

**Figures S4 & S5**:: Basinwide trends in first year ice extent as a fraction of total extent and mW99 SWE fields from 2003-2018 are made using Ice_type_analysis_and_testing.ipynb

**Figure S6 to S12**: made using Regional_W99_vs_SMv2.ipynb

**Figure S13** made using SM_Climatology.ipynb

**Figure S14 to S19**: made using Regional_W99_vs_SMv2.ipynb
