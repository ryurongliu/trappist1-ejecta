# Impact Ejecta Transfer in the TRAPPIST-1 System
Investigating impact ejecta transfer in the TRAPPIST-1 system through simulated planetary collisions, with Dr. Caleb Scharf at Columbia University.  
This code makes heavy use of [Hanno Rein's REBOUND N-body integration package](https://github.com/hannorein/rebound). 

## Method
We simulated the TRAPPIST-1 system and generate impact ejecta at the surface of planet d. Ejecta were given initial velocities of v_i = v_escape + v_increment, with v_escape = 7.856 km/s and v_increment = [0, 1, 3, 4, 5] km/s. The MERCURIUS integrator accurately simulates massless test particles without affecting planetary motion, so simulations can be aggregated. For each v_increment, we ran 60 simulations of 5,000 ejecta each for 2,000 years.   
**In total, each v_increment simulation has 300,000 ejecta integrated over 2,000 years.**   
Simulations were performed in batches using Columbia University's terremoto computing cluster and the slurm job scheduling system.

## Overview
- **sim_templates/** contains python and slurm templates for running simulations.
- **used_scripts/** contains the python and slurm scripts for specific v_increments.
- **analysis_tools/** contains modules for processing and analyzing output data.

Example plots:  
![overview_percentages_of_total_histogram](https://user-images.githubusercontent.com/84996423/133484243-8c4e6e55-b56a-4136-bcbc-af95ad981a71.png)
![300000e_2000y_4vinc_g_cols_v_time](https://user-images.githubusercontent.com/84996423/133484337-128612dc-ef51-4865-b79e-f1aaf131b9ac.png)
![ezgif com-gif-maker](https://user-images.githubusercontent.com/84996423/133485125-dcaa7206-f065-4e2a-b24c-72af3f6f42be.gif)


## Documentation
[IN PROGRESS] - This code will be eventually generalized to create an end-to-end pipeline for simulating, processing, and analyzing impact ejecta in any exoplanetary system.  

### Simulation
1. Copy start_template.py and rename it to [#ejecta]e_[#years]y_[#velocity increment]vinc.py 
2. Edit lines 309-xxx to input simulation variables
      - num_ejecta: number of ejecta
      - num_years: number of years to integrate
      - v_increment: velocity increment in km/s
      - sourceplanet: choose from ['b', 'c', 'd', 'e', 'f', 'g', 'h']
      - archive_int: time interval (years) per archive snapshot; recommended 10yr
    - IF CPU TIME IS LIMITED:
      - chunk: how many years to integrate at a time
      - proj_chunktime: how long it takes to integrate each chunk (projected)
      - maxtime: maximum time you have on the CPU
3. copy start_template.sh and rename it the same way (with .sh)
4. Edit the .sh file to reflect the python file name, and how many iterations you want to run
5. Submit job to slurm  
Output data will be organized like so:  
[Ejecta_Simulation_Data]
- []e_[]y_[]vinc_[sim_num]
  - ........_end.bin : 
  - ........_overview.bin
  - ........_
