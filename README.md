# README #

### Active Adherent Vertex Model (AAVM) ###

##### as detailed in : #####
#### Cooperation of dual modes of cell motility promotes epithelial stress relaxation to accelerate wound healing, arXiv:1808.01954 (2018) ####

### Authors / Contributors ###

* Michael F Staddon (University College London)
* Shiladitya Banerjee (University College London)

#### created at the University College London ####

### System Requirements ###

This system requires Surface Evolver 2.70 which can be downloaded at: http://facstaff.susqu.edu/brakke/evolver/evolver.html

### QUICKSTART GUIDE ###

Create a new directory for the simulation, containing the "wound_healing.fe", "parameters.inp", "dynamics.secmd", and "wound_creation.secmd" files. 

The "wound_healing.fe" file is the main Surface Evolver file, containing the tissue and substrate geometries, energy definitions, and code to run the simulation.

The "parameters.inp" file contains the system parameters. These are input as dimensional, and made dimensionless while running in Surface Evolver.

The "dynamics.secmd" contains general simulation commands which numerically solve the dynamics of the system, and record simulation statistics.

The "wound_creation.secmd" contains commands related to the create of the wound in the tissue.

Create folders "/output/", for simulation statistics, and "/output/images/", for simulation images, in the directory.

Run the simulation. On Windows double clicking the "wound_healing.fe" file should run it. On mac use the command line e.g.,
```
> evolver wound_healing.fe
```

During running, the simulation records statistics every "record_interval" time steps. Once the simulation has completed, the following output files will have been created, where %s is the "output_name" variable:

* "output/displacement_%s_%06d.csv" // for where %06d is the simulation step with leading zeros. This contains the substrate node positions at the given recorded simulation step. Row i contains the x, y positions of substrate node i.

* "output/wound_area.csv" // the current simulation step and the wound area.

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
|kappa|float|0.2|nN um^(-3)|Cell elastic modulus|
|gamma|float|20|nN um^(-1)|Cell contractility|
|pzero|float|3.6||Cell preferred shape index|
|**Cell motility**|||||
|protrusion_force|float|2000|nN|Protrusive force during cell crawling|
|V0|float|10/3600|um s^(-1)|Internal motility speed|
|DR|float|5/3600|s^(-1)|Cell polarity rotational diffusion|
|**Purse-string**|||||
|purse_string_tension|float|300|nN|Tension on purse-string edges on the wound|
|purse_strin_rate|float|4/3600|um s^(-1)|Transition rate from crawling to purse-string on wound edge cells|
|**Adhesion**|||||
|kon|float|500/3600|s^(-1)|Adhesion binding rate|
|koff|float|25/3600|s^(-1)|Adhesion unbinding rate|
|max_binding_distance|float|1.5|um|Maximum length between cell and substrate that an adhesion can bind too|
|focal_stiffness|float|80|nN um^(-1)|Focal adhesion spring stiffness|
|**Substrate**|||||
|substrate_youngs|float|4|kPa|Substrate Young's modulus|
|substrate_height|float|5|um|Substrate height|
|**Wound options**|||||
|wound_radius|float|15|um|Radius of the wound|
|wound_aspect_ratio|float|1||Aspect ratio of the wound. Wounds are elliptical with area pi * radius^2 and this aspect ratio|
|**Other**|||||
|viscocity|float|7200|nN um^(-1) s|Viscosity used in overdamped equations|
|dt|float|3.6|s|Simulation time step|
|lt1|float|0.5|um|Minimum edge length for a T1 transition to occur|
|lmin|float|1.0|um|Minimum cell dge length. Shorter edges will merge with neighbouring edges, if possible|
|lmax|float|5.0|um|Maximum cell edge length. Longer edges will be subdivided|
|random_seed|int|1||Simulation random seed|
|img_output_interval|int|20||Number of time steps between recording images|
|record_interval|int|20||Number of time steps between recording statistics|
|output_name|string|"wound_healing"||Identifying name for output files|

### Contribution guidelines ###

* Email: shiladitya.banerjee@ucl.ac.uk

### Who do I talk to? ###

* Michael Staddon (michael.staddon.16@ucl.ac.uk)
* Shiladitya Banerjee (shiladitya.banerjee@ucl.ac.uk)
