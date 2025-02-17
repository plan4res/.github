# plan4res

This github organisation contains everything to install and run plan4res
All documentation is available in https://github.com/plan4res/documentation

## Install plan4res
It is recommended to install on linux (for Windows users, install in WSL), with the full plan4res environment
This requires at least 3Gb
Clone the installation scripts in https://github.com/plan4res/install and run:
    ./plan4res_install.sh 
See possible options in documentation or ./plan4res_install.sh -H

If data are stored in a different repository, or you are installing on a server, configure your user account by running
    ./user_init_plan4res -D P4R_INSTALL_DIR
See possible options in documentation or ./user_init_plan4res.sh -H

## Run plan4res
Create your dataset, taking inspiration from the examplary dataset installed together with plan4res installation, in the repo where you installed plan4res, and in case you configured a user account, in the chosen repo, under data/toyDataset
See userManual for details about how to run plan4res

Create a plan4res dataset out of IAMC input data and timeseries: p4r CREATE toyDataset
Create NetCDF data for SSV (required by SMS++) out of plan4res csv data: p4r FORMAT toyDataset -M optim
Run the Seasonal Storage Valuation (SSV): p4r SSV toyDataset
Create NetCDF data for SIM (required by SMS++) out of plan4res csv data: p4r FORMAT toyDataset -M simul
Run the simulation (SIM): p4r SIM toyDataset
Create NetCDF data for CEM (required by SMS++) out of plan4res csv data: p4r FORMAT toyDataset -M invest
Run the capacity expansion (CEM): p4r CEM toyDataset
Run a workflow with data creation, data formatting, models runs: p4r SSVandSIM   or p4r SSVandCEM

