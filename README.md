# _Elastic buildings: Calibrated district-scale simulation of occupant-flexible campus operation for hybrid work optimization_

[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)  ![Python Version](https://upload.wikimedia.org/wikipedia/commons/a/a5/Blue_Python_3.8_Shield_Badge.svg)

This repository contains the research compendium for our paper:

> Mart\'in Mosteiro-Romero, Clayton Miller, Adrian Chong, and Rudi Stouffs (2022).
> Elastic buildings: Calibrated district-scale simulation of occupant-flexible campus operation for hybrid work optimization.
> Submitted to _Building and Environment_.

The compendium includes all the data and code needed to reproduce the analysis and figures associated with the publication.

## Documentation

This GitHub repository comprises the following files and folders:
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


## Repository Structure
```
./
├── full_paper_workflow.ipynb                     # Jupyter notebook with the code and documentation to replicate this study
├── meter_data                                    # 
│   └── cooling_kWh_2018-2020.csv                 # csv file containing the hourly cooling demand by for each building for the period 2018-2020
│   └── electricity_kWh_2018-2020.csv             # csv file containing the hourly electricity demand by for each building for the period 2018-2020
│   └── occupancy_wifi_2018-2020.csv              # csv file containing the hourly number of devices connected to the WiFi network by building for the period 2018-2020
│   └── weather_2018_and_2020.csv                 # csv file containing measured weather station data for the years 2018 and 2020
├── CEA_model                                     # directory containing the CEA models developed in this study; please refer to the [CEA documentation](https://city-energy-analyst.readthedocs.io/en/latest/) for the documentation of each individual file
│   ├── baseline                                  # baseline model of the university campus using archetypal CEA inputs for the years 2018 and 2020
│   │   ├── 2018                                  # 
│   │   │   └── inputs                            # 
│   │   │       └── building-geometry             # 
│   │   │       │   └── site.shp, site.*          # shapefile containing a polygon showing the extents of the site under consideration
│   │   │       │   └── surroundings.shp          # shapefile of the footprints and building heights of buildings surrounding the site
│   │   │       │   └── zone.shp, zone.*          # shapefile of the footprints and building heights of buildings within the site
│   │   │       └── building-properties           # 
│   │   │       │   └── air_conditioning.dbf      # dbf file containing the properties of the HVAC systems in each building
│   │   │       │   └── architecture.dbf          # dbf file containing the architectural properties of each building (e.g., U-values, window-to-wall ratios, etc.)
│   │   │       │   └── indoor_comfort.dbf        # dbf file containing the operating parameters of the HVAC systems in each building
│   │   │       │   └── internal_loads.dbf        # dbf file containing the various internal gains in each building
│   │   │       │   └── supply_systems.dbf        # dbf file containing the properties of the systems supplying each building
│   │   │       │   └── typology.dbf              # dbf file containing the functional mix and typology of each building
│   │   │       │   └── schedules                 #
│   │   │       │       └── *.csv                 # csv file containing the operating schedules of a given building in the case study area
│   │   │       └── networks                      # 
│   │   │       │   └── streets.shp, streets.*    # shapefile of the streets within the site (not used in this study)
│   │   │       └── technology                    # CEA databases imported when creating a CEA model; please refer to the [CEA documentation](https://city-energy-analyst.readthedocs.io/en/latest/) for the documentation of each individual file
│   │   │       │   └── archetypes                # 
│   │   │       │   └── assemblies                # 
│   │   │       │   └── components                # 
│   │   │       └── topography                    # 
│   │   │       │   └── terrain.tiff              # digital elevation model of the case study area (assumed flat in this case study)
│   │   │       └── weather                       # 
│   │   │           └── weather.epw               # weather file used in this scenario
│   │   │           └── future_scenarios          # weather files for future climatic scenarios
│   │   │               └── weather-TMY.epw       # typical meteorological year weather file
│   │   │               └── weather-2020.epw      # weather file generated by using `weather-TMY.epw` as an input to the R package [epwshiftr](https://github.com/ideas-lab-nus/epwshiftr)
│   │   │               └── weather-2040.epw      # weather file generated by using `weather-TMY.epw` as an input to the R package epwshiftr
│   │   │               └── weather-2060.epw      # weather file generated by using `weather-TMY.epw` as an input to the R package epwshiftr
│   │   ├── 2020                                  # 
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   ├── calibration                               # calibrated CEA model of the university campus for the years 2018 and 2020
│   │   ├── 2018                                  # 
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   ├── 2020                                  # 
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   ├── first_run                             # calibration assessment metrics for the first run of the calibration procedure
│   │   │   ├── cvrmse_min.csv                    # minimum CV(RMSE) of the modeled total cooling (QC_sys_kWh), space cooling (Qcs_sys_kWh), and electricity demand (E_sys_kWh) along with the combination of input parameters that leads to that CV(RMSE) for each building
│   │   │   ├── nmbe_min.csv                      # minimum NMBE of the modeled total cooling (QC_sys_kWh), space cooling (Qcs_sys_kWh), and electricity demand (E_sys_kWh) along with the combination of input parameters that leads to that NMBE for each building
│   │   ├── second_run                            # calibration assessment metrics for the second run of the calibration procedure
│   │   │   └── ...                               # (see .\CEA_model\calibration\first_run for file description)
│   ├── regression                                # calibrated CEA model of the university campus after using the regression model for electricity for the years 2018 and 2020
│   │   ├── 2018                                  # 
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   ├── 2020                                  # 
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   └── regression_results_with_10-Fold_CV.csv# regression parameters and evaluation of the regression model adequacy for each building
│   ├── baseline_calibration_regression_comparison# summary of the comparison metrics for each of the versions of the CEA model
│   │   └── comparison_CVRMSE_Cooling.csv
│   │   └── comparison_CVRMSE_Electricity.csv
│   │   └── comparison_NMBE_Cooling.csv
│   │   └── comparison_NMBE_Electricity.csv
│   ├── scenarios                                 # CEA model for each of the scenarios considered
│   │   └── baseline                              # scenario with 0% working from home (WFH) -- i.e., 100% occupancy -- and normal building operation
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   └── WFH-0.25                              # scenario with 75% occupancy and normal building operation
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   └── WFH-0.5                               # scenario with 50% occupancy and normal building operation
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   └── WFH-0.75                              # scenario with 25% occupancy and normal building operation
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   └── WFH-0.25-Ns                           # scenario with 75% occupancy and occupant-driven building controls
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   └── WFH-0.5-Ns                            # scenario with 50% occupancy and occupant-driven building controls
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   └── WFH-0.75-Ns                           # scenario with 25% occupancy and occupant-driven building controls
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   └── WFH-0.25-closed_buildings             # scenario with 75% occupancy and elastic space allocation
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   └── WFH-0.5-closed_buildings              # scenario with 50% occupancy and elastic space allocation
│   │   │   └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   │   └── WFH-0.75-closed_buildings             # scenario with 25% occupancy and elastic space allocation
│   │       └── ...                               # (see .\CEA_model\baseline\2018 for folder structure)
│   └── 0_daysim_binaries                         # [Daysim](https://github.com/MITSustainableDesignLab/Daysim) binaries required to run the CEA radiation script. These are included in the CEA installation package
│   └── location_geocode.csv                      # Dataset with locations and their longitude and lattitude
└── plots                                         # plots generated using full_paper_workflow.ipynb
```

## Requirements
This workflow requires a few different packages to be installed, most importantly the City Energy Analyst v3.27.0. CEA includes the majority of the packages required to replicate this work, except a few additional ones:

- [City Energy Analyst v3.27.0](https://github.com/architecture-building-systems/CityEnergyAnalyst/releases/tag/v3.27.0)
- `sklearn`
- `holidays`
- `july`

## Citation

Please cite this compendium as:
```
@article{mosteiro_romero_2022,
  title={Elastic buildings: Calibrated district-scale simulation of occupant-flexible campus operation for hybrid work optimization},
  author={Mart\'in Mosteiro-Romero and Clayton Miller and Adrian Chong and Rudi Stouffs},
  journal={Submitted to Building and Environment},
}
```

## License

MIT License

Copyright (c) 2022 Building and Urban Data Science (BUDS) Group and National University of Singapore (NUS)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

