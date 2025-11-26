# IrrigationExtentMapping

Scripts implementing a full Google Earth Engine workflow for mapping irrigation extent using Landsat imagery and OPTRAM soil moisture (Sadeghi et al., 2017), without relying on training data.
The workflow is modular, allowing you to run the entire pipeline or individual steps depending on your needs.

# Overview

This repository provides tools to:

Derive OPTRAM soil-moisture parameters for any Landsat WRS Path/Row (2000–2024)

Compute OPTRAM soil moisture for each Landsat image

Compare OPTRAM soil moisture to SMAP for optional quality control

Map annual irrigation extent

Design sampling and perform accuracy assessments

All scripts are written for use in Google Earth Engine (GEE).

# Add in Google Earth Engine
To add the repository in Google Earth Engine directly you can click on the following link
https://code.earthengine.google.com/?accept_repo=users/Esmaeel-ad/IrrigationExtentMapping

# Repository Structure
## 01_CalculateSM_OptramParameters

Calculates OPTRAM soil-moisture parameters for a specified WRS Path and Row.

Uses the stepwise SRT–NDVI relationship

Fits a linear model to estimate the parameters iw, id, sd, sw, vw, and wv

Computes parameters for each year from 2000–2024 using two years of Landsat data

Output: A FeatureCollection containing OPTRAM parameters for each year
Find the file OptramParsameters.csv for all pre-calculated pararmeters than can be used directly in step 04 

## 02_RawLandsatToSM_Optram

Optional quality-control step that computes OPTRAM soil moisture for every Landsat image in the selected footprint.

Requires the parameter file generated in Step 01

Inputs: year, WRS path, and WRS row

Output: OPTRAM soil-moisture images for each Landsat acquisition in that year

## 03_CompareOptramSMToSMAP

Optional quality-control step comparing OPTRAM soil moisture (Step 02) to SMAP soil moisture.

Matches OPTRAM SM images with SMAP data on the same dates

Aggregates OPTRAM SM to SMAP pixel size

Computes R², RMSE, p-value, slope, and intercept

Supports optional generation of per-image scatterplots

Covers all years from 2000–2024

## 04_OptramSMToIrrigationExtent

Main script for generating irrigation-extent maps.

Uses OPTRAM soil moisture parameters calculated from Step 01 (OptramParsameters.csv) Or saved soil moisture from Step 02

Output: Annual raster classification with the following codes:

0 = Not irrigated

1 = Irrigated in summer

2 = Irrigated every year

3 = Irrigated in winter

## 05_AccuracyAssessment_SamplingDesign

Optional quality-control step that generates random reference points for accuracy assessment.

## 06_AccuracyAssessment_ResponseDesign

Optional quality-control step documenting the response-design process used to label reference points.

## 07_AccuracyAssessment_Analysis

Optional quality-control step that computes accuracy metrics for dry-season irrigation extent for each year.

Requires labeled reference points

Outputs include overall accuracy, F-score, and user/producer accuracy for irrigated and non-irrigated classes

# License

See LICENSE.md for terms of use.

# Summary

This repository provides a complete, reproducible workflow for mapping irrigation extent using OPTRAM soil moisture and Landsat time series without training data.
