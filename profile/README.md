# plan4res

This github organisation contains everything to install and run plan4res.

All documentation is available in https://github.com/plan4res/documentation

Plan4res is an electricity system optimisation and simulation tool, composed of the 3 following models:

- A Capacity expansion model (CEM) aimed at adapting the electricity mix - meaning optimising the mix to fit to the demand. CEM will determine new power generation, storage and interconnections capacities, minimising the sum of the investment cost and the average operation cost on a chosen year.
- A seasonal storage valuation model (SSV) aimed at optimising the management of seasonal storages. SSV will compute "water values" which will be used by both CEM and SIM in order to give a value to the water, allowing use of the water when it is optimal (usually in periods with high demand) 
- A simulation tool, based on a Unit Commitment model (SIM), aimed at optimising the operation of the system. SIM will compute the schedules of all assets (generation, storage, flows on interconnections), usually on a whole year with hourly timestep.

plan4res is composed of:
- an environment for running the different modules: p4r-env. This was developed by CRAY Switzerland and HPE Switzerland during the plan4res project (see https://gitlab.com/cerl/plan4res/p4r-env)
- the main modules for modelling, simulating and optimising a power system, which are based on the SMS++ library developed by University of Pisa (see https://gitlab.com/smspp/smspp-project)
- tools for data treatment and visualisation (python scripts in github.com/plan4res/plan4res-scripts); These tools are using the pyam-iamc module developped by IIASA (see https://pyam-iamc.readthedocs.io/en/stable/index.html)
- scripts for managing workflows and running all the modules (see github.com/plan4res/include)

## Install plan4res
It is recommended to install on linux (for Windows users, install in WSL), with the full plan4res environment p4r-env
This requires at least 3Gb
Clone the installation scripts in https://github.com/plan4res/install and run:
    ./plan4res_install.sh 
See possible options in documentation or ./plan4res_install.sh -H

If data are stored in a different repository, or you are installing on a server, configure your user account by running
    ./user_init_plan4res -D P4R_INSTALL_DIR
See possible options in documentation or ./user_init_plan4res.sh -H

## Run plan4res
Create your dataset, taking inspiration from the examplary dataset installed together with plan4res installation, in the repo where you installed plan4res, and in case you configured a user account, in the chosen repo, under data/toyDataset
This example dataset is also available [here](https://github.com/plan4res/toyDataset)

See userManual for details about how to run plan4res

- Create a plan4res dataset out of IAMC input data and timeseries: p4r CREATE toyDataset
- Create NetCDF data for SSV (required by SMS++) out of plan4res csv data: p4r FORMAT toyDataset -M optim
- Run the Seasonal Storage Valuation (SSV): p4r SSV toyDataset
- Create NetCDF data for SIM (required by SMS++) out of plan4res csv data: p4r FORMAT toyDataset -M simul
- Run the simulation (SIM): p4r SIM toyDataset
- Create NetCDF data for CEM (required by SMS++) out of plan4res csv data: p4r FORMAT toyDataset -M invest
- Run the capacity expansion (CEM): p4r CEM toyDataset
- Run a workflow with data creation, data formatting, models runs: p4r SSVandSIM   or p4r SSVandCEM


## 📬 Contact
👉 [Fill this contact form](https://plan4res.github.io/contact/contact.html) 



