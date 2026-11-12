# XGBoost_hail
This repository contains the code for hail proxy extraction.
ERA5_hail_proxies_extraction_newSRH03.py is used to extract the following variables from ERA-5 ['CAPEmax', 'SRH03', 'VS03', 'FLH'] 
New_Hail_proxies_extraction.py is the code used to derive the values of ['CINmax', 'SRH06', 'VS06', 'DewT', 'TotalTotals', 'RH850', 'RH500'] from ERA-5.
create_annual_predictors_files.py is used to save these predictors in yearly files, making it ready to use by the models.
The XGB models can be found at https://zenodo.org/uploads/24148709.
