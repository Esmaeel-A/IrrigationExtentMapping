#IrrigationExtentMapping

Scripts implementing a full Google Earth Engine workflow for mapping irrigation extent using Landsat imagery and OPTRAM soil moisture (Sadeghi et al., 2017), without relying on training data.
The workflow is modular, allowing you to run the entire pipeline or individual steps depending on your needs.

Overview

This repository provides tools to:

Derive OPTRAM soil-moisture parameters for any Landsat WRS Path/Row (2000–2024)

Compute OPTRAM soil moisture for each Landsat image

Compare OPTRAM soil moisture to SMAP for quality control

Map irrigation extent annually

Design and run accuracy assessments

All scripts are written for use in Google Earth Engine (GEE).

Repository Structure
01_CalculateSM_OptramParameters

Calculates OPTRAM soil-moisture parameters for a specified WRS Path/Row.

Uses the stepwise SRT–NDVI relationship

Fits a linear model to estimate OPTRAM parameters (iw, id, sd, sw, vw, wv)

Parameters are computed for each year from 2000–2024 using two years of Landsat data

Output: FeatureCollection of OPTRAM parameters for all years

02_RawLandsatToSM_Optram

Quality-control step (optional).
Computes OPTRAM soil moisture for every Landsat image in the selected footprint.

Requires parameter file from Step 01

Inputs: year, WRS path, WRS row

Output: OPTRAM soil-moisture image for each Landsat acquisition in the chosen year

03_CompareOptramSMToSMAP

Quality-control step (optional).
Compares OPTRAM soil moisture (Step 02) with SMAP soil moisture.

Matches each OPTRAM SM image with SMAP on the same date

Aggregates OPTRAM SM to SMAP pixel scale

Computes R², RMSE, p-value, slope, and intercept

Optional: generate scatter plots

Covers all years from 2000–2024

04_OptramSMToIrrigationExtent

Main step for mapping irrigation extent.

Uses OPTRAM SM computed on the fly (Step 01) or pre-computed SM (Step 02)

Output: Yearly categorical raster with values:

0 = Not irrigated

1 = Irrigated in summer

2 = Irrigated all years

3 = Irrigated in winter

05_AccuracyAssessment_SamplingDesign

Quality-control step (optional).
Generates random reference points for accuracy assessment.

06_AccuracyAssessment_ResponseDesign

Quality-control step (optional).
Documentation and design for labeling reference points.

07_AccuracyAssessment_Analysis

Quality-control step (optional).
Computes accuracy metrics for dry-season irrigation extent for each year.

Requires labeled reference points

Outputs include overall accuracy, F-score, and user/producer accuracy for irrigated and non-irrigated classes

License

See LICENSE.md for details.

Summary

This repository provides a complete and reproducible workflow for mapping irrigation extent using OPTRAM soil moisture and Landsat time series without training data. Scripts can be used sequentially or independently depending on your application.
