This branch of ufs_weather_model contains bug fixes and modifications to run the weather model on a cartesian grid with periodic boundary conditions. 

The model is run in the same manner as when it's run on a cubed-sphere grid (i.e., global, regional), except no boundary conditions are required. 

Initial conditions are provided as output from chgres_cube. All provided sample data are on a 98x98 3-km grid with 48 vertical levels and Thompson tracers. Each environment has a 10-km horizontal radius, 2-km vertical radius, 3-K bubble placed nearthe center of the domain over a background Weisman-Klemp 1984 thermodynamic sounding. 

This data and a sample input.nml file can be accessed on Hera at

/scratch1/BMC/gsd-fv3/Larissa.Reames/ideal_input

Data should be copied or linked directly from this location. No need to change the file names, they are as they should be.

Two variations on the wind shear environment are provided. Subdirectories are as follows:

    nowind_thermal: 0 wind everwhere

    quarter_circle_supercell : Standard quarter-circle hodograph with a final wind vector aloft of (27.15, 3.5). This is the hodograph provided in WRF's quarter-circled supercell idealized sounding.

Important changes to input.nml that should be noted:

    - A new section, &test_case_nml : This includes the "test_case" option. Do not change from 999. You will have a bad time if you do.

    - New/different options in &fv_core_nml:

        ~ grid_type = 4 : This tells the model to run on a cartesian grid with periodic boundary conditions

        ~ dx_const, dy_const = 3000. : Horizontal grid size. Leave at 3-km as long as you're using the provided input data

        ~ deglat = 0. : Latitude to use for coriolis calculations. Suggested to leave at 0. to eliminate coriolis.

        ~ external_ic = .false. : This won't be used if grid_type = 4. Keep false.

        ~ ideal_external_ic = .true. : This option was added to initialized the cartesian grid from the provided input data. Keep .true.

    - Note the namelist is not set up to use the write component, so data will be written in a single file, fv3_history.nc , at the end of the run. Using the write component with a cartesion grid is an untested configuration, and it probably would not work well as the write component requires an output lat/lon grid specification and the computations are done on a cartesian grid.

For any additional questions, contact Larissa Reames at larissa.reames@noaa.gov.
