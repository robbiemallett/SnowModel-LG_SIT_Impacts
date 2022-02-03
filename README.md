# Code repository for Mallett et al. (2021; The Cryosphere)

## Introduction

This repository contains all the code necessary for replication of Mallett et al. (2021).

## Overview of steps to reproduce the sea ice thickness data

- Download daily ice-type data, average to monthly and regrid
  (cds_daily_to_monthly_and_regrid.ipynb)
- Make monthly mW99 2002-2018
  (mW99_maker.ipynb)
- Download daily SnowModel-LG data and average to monthly
  (SM_daily_to_monthly.ipynb)
- Download radar freeboard data from CCI & AWI
- Calculate thickness components from both snow data sets (and Nesosim if you want), and also the radar freeboard data
  (Calculate_thickness_components.ipynb)

## Overview of steps to reproduce the main figures

**Figure 1**: The regions of the Arctic Ocean are defined using XXX.ipynb

**Figure 2**

**Figure 3**

**Figure 4**

**Figure 5**

**Figure 6**

**Figure 7**

**Figure 8**

**Figure 9**

**Figure 10**

**Figure 11**

## Overview of steps to reproduce the supplementary figures

**Figure S1**: Value of the propagation factor used to convert radar freeboard to ice freeboard, plotted as a function of snow density

**Figure S2**: The number of valid, 25×25 km radar-freeboard grid cells in each region for each month

**Figure S3**: Difference in snow depth in SnowModel-LG when driven by ERA5 and Merra2 reanalysis data 

**Figure S4**: Basinwide trends in first year ice extent as a fraction of total extent from 2003-2018

**Figure S5**: Basinwide trends in mW99 SWE fields from 2003-2018

**Figure S6**: Detrended timeseries of spatially averaged snow contributions to sea ice thickness by region from W99 and
SnowModel-LG

**Figure S7** Same as S6 but over just first year ice

**Figure S8** Same as S6 but over just multi-year ice

**Figure S9**

**Figure S10**

**Figure S11**

**Figure S12**

**Figure S13**

**Figure S14**

**Figure S15**

**Figure S16**

**Figure S17**

**Figure S18**

**Figure S19**
