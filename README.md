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

## Documentation
[IN PROGRESS] - This code will be generalized to create an end-to-end pipeline for simulating, processing, and analyzing impact ejecta in any exoplanetary system. 
