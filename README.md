# SoilMoistureProfiles
 The code computes vertical soil moisture profiles for conceptual **(e.g., CFE)** and layered **(e.g., LGAR)** soil revervoirs.
 Inputs include **total soil moisture storage** and change in the **soil moisture storage per timestep**
 For conceptual reservoir, the algorithm has two steps.
  * Find water table location using Netwon iterative scheme
  * Use Clap-Hornberger soil moisture characteristic function to compute vertical profile
 For layered soil reserviors, the two options include 
  * constant by layer, and Clap-Horngerger soil moisture characteristic function for the profile below the depth of the last layer
  * linearly interpolated profile between consecutive layers, and Clap-Horngerger soil moisture characteristic function for the profile below the depth of the last layer
  
## Standalone run:
 * run [make_bmi_coupler.sh](https://github.com/NOAA-OWP/SoilMoistureProfiles/blob/main/make_bmi_coupler.sh) to get the executable (e.g., run_bmi_coupler)
 * run ./run_bmi_coupler test/config.txt

## Coupled mode:
 * Coupling SoilMoistureProfiles to any module (for instance, CFE or SFT) **must** follow these [instructions](https://github.com/NOAA-OWP/SoilFreezeThaw/tree/ajk/sft_only) for building and running
 * Follow this example: [couple SMP with SFT](https://github.com/NOAA-OWP/SoilFreezeThaw/blob/master/src/main_cfe_aorc_pet_ftm.cxx)

## Options in the config file
* `smcmax` (porosity; maximum moisture content), `b`, `satpsi` (saturated matric potential) are needed for the soil moisture characteristic function
* `Z` is the soil layer thickness (for instance, if SMP is coupled with SFT then this `Z` is the vertical resolution of the SFT model)
* `smc_profile` = `conceptual` if conceptual model(e.g., CFE) or `layered` if layered based soil moisture model is used (e.g., LGAR)
* if `smc_profile` = `layered`, then set `smc_profile_option` = `constant` for layered-constant profile or `linear`  for linearly interpolated profile between layers
* `water_table` depth of the initial water table
