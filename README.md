# _Elastic buildings: Calibrated district-scale simulation of occupant-flexible campus operation for hybrid work optimization_
# Documentation

This repository contains all the inputs required to replicate the work done in this paper, namely:
1. `full_paper_workflow.ipynb`: Jupyter notebook with the code and documentation to replicate this study
2. `meter_data`
  1. Hourly cooling demand by building for the period 2018-2020
  2. Hourly electricity demand by building for the period 2018-2020
  3. Hourly number of devices connected to the WiFi network by building for the period 2018-2020
  4. Weather station data for the years 2018 and 2020
3. `CEA_model`: [City Energy Analyst (CEA)](https://github.com/architecture-building-systems/CityEnergyAnalyst) models 
  1. `baseline`: Inputs to the CEA model of the university campus using archetypal CEA inputs for the building properties
  2. `calibration`: Inputs to the calibrated CEA model of the university campus for the years 2018 and 2020, as well as the previously-run calibration assessment metrics for two runs of the calibration procedure
  3. `regression`: Inputs to the calibrated CEA model of the university campus after using the regression model for electricity for the years 2018 and 2020, as well as the previously-run regression model assessment metrics
  4. `baseline_calibration_regression_comparison`: Summary of the comparison metrics for each of the versions of the CEA model
  5. `scenarios: Inputs to the CEA model for each of the scenarios considered for the years 2018 and 2020
  6. `0_daysim_binaries`: [Daysim](https://github.com/MITSustainableDesignLab/Daysim) binaries required to run the CEA radiation script. These are included in the CEA installation package.
4. `plots`: Plots included in the paper, which are generated in the `full_paper_workflow.ipnyb` notebook.

This workflow requires a few different packages to be installed, most importantly the City Energy Analyst. You can find an installation guide [here](https://city-energy-analyst.readthedocs.io/en/latest/installation/installation.html).
