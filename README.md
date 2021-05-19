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

## Overview of steps to reproduce the analysis





