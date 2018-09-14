# README #

### Active Adherent Vertex Model (AAVM) ###

##### as detailed in : #####
#### Force localization modes in dynamic epithelial colonies, MBoC (2018) ####

### Authors / Contributors ###

* Michael F Staddon (University College London)
* Shiladitya Banerjee (University College London)

#### created at the University College London ####

### System Requirements ###

This system requires Surface Evolver 2.70 which can be downloaded at: http://facstaff.susqu.edu/brakke/evolver/evolver.html

### QUICKSTART GUIDE ###

Create a new directory for the simulation, containing the "micropattern.fe", "parameters.inp", and "dynamics.secmd" files. 

The "micropattern.fe" file is the main Surface Evolver file, containing the tissue and substrate geometry, energy definitions, and code to run the simulation.

The "parameters.inp" file contains the system parameters. These are input as dimensional, and made dimensionless before running in Surface Evolver.

The "dynamics.secmd" contains general simulation commands which numerically solve the dynamics of the system, and record simulation statistics.

Create folders "/output/", for simulation statistics, and "/output/images/", for simulation images, in the directory.

Run the simulation. On Windows double clicking the "micropattern.fe" file should run it. On mac use the command line e.g.,
```
> evolver micropattern.fe
```

During running, the simulation records statistics every "record_interval" time steps. Once the simulation has completed, the following output files will have been created, where %s is the "output_name" variable:

* "output/displacement_%s_%06d.csv" // for where %06d is the simulation step with leading zeros. This contains the substrate node positions at the given recorded simulation step. Row i contains the x, y positions of substrate node i.

* "output/cell_center_%s.csv" // the cell centers at each recorded time step. Columns (i\*2, i\*2 + 1) contains the (x, y) position of cell i's center.

* "output/colony_boundary_%s_%06d.csv" // the positions of vertices on the boundary of the cell colony. Each row contains the x, y position of a different node. The node corresponding to a certain row can be different for different simulation steps. This gives the border shape of the cell colony.

* "output/images/%s_%06d.ps" //post script images of the simulation, recorded every "image_interval" time steps.


## Simulation Parameters ##

Simulation parameters may be changed in the "parameters.inp" file. Alternatively, values can be overwritten in the simulation file by writing them under the line "read "parameters.inp";" e.g.,
```
read "parameters.inp";
pzero := 3.0;
```
allowing several simulation files with different parameters in the same folder.

|Variable name              |Type   |Default value  |Units  |Description                        |
|-------------              |:----: |:-------------:|:-----:|-----------------------------------|
|**Tissue properties**|||||
|kappa|float|0.0666|nN um^(-3)|Cell elastic modulus|
|gamma|float|15|nN um^(-1)|Cell contractility|
|pzero|float|3.6||Cell preferred shape index|
|colony_tension|float|112.5|nN|Additional line tension on the colony boundary|
|**Cell motility**|||||
|protrusion_force|float|1125|nN|Protrusive force during cell crawling|
|V0|float|30/3600|um s^(-1)|Internal motility speed|
|DR|float|10/3600|s^(-1)|Cell polarity rotational diffusion|
|**Adhesion**|||||
|kon|float|500/3600|s^(-1)|Adhesion binding rate|
|koff|float|50/3600|s^(-1)|Adhesion unbinding rate|
|max_binding_distance|float|3|um|Maximum length between cell and substrate that an adhesion can bind too|
|focal_stiffness|float|60|nN um^(-1)|Focal adhesion spring stiffness|
|**Substrate**|||||
|substrate_youngs|float|4|kPa|Substrate Young's modulus|
|substrate_height|float|7.5|um|Substrate height|
|**Micropattern shape**|||||
|pattern_area|float|6750|um^2|Total area where the cell can adhere to the substrate|
|pattern_curvature|float|36.75|um|Radius of the curved regions of the micropattern. The micropattern takes a stadium shape.|
|**Other**|||||
|viscocity|float|2700|nN um^(-1) s|Viscosity used in overdamped equations|
|dt|float|1.8|s|Simulation time step|
|lt1|float|1.5|um|Minimum edge length for a T1 transition to occur|
|lmin|float|1.5|um|Minimum cell dge length. Shorter edges will merge with neighbouring edges, if possible|
|lmax|float|7.5|um|Maximum cell edge length. Longer edges will be subdivided|
|random_seed|int|1||Simulation random seed|
|img_output_interval|int|100||Number of time steps between recording images|
|record_interval|int|100||Number of time steps between recording statistics|
|output_name|string|"micropattern"||Identifying name for output files|

### Contribution guidelines ###

* Email: shiladitya.banerjee@ucl.ac.uk

### Who do I talk to? ###

* Michael Staddon (michael.staddon.16@ucl.ac.uk)
* Shiladitya Banerjee (shiladitya.banerjee@ucl.ac.uk)
