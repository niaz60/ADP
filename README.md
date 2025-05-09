# Auto Diffraction Pipeline (ADP):
--------------------------------------------------------------------------------------------
## Description
The Auto Diffraction Pipeline (ADP) is a Python-based framework designed to generate synthetic 1D and 2D X-ray diffraction (XRD) patterns from Crystallographic Information Files (CIFs). It enables automated, high-throughput simulation of diffraction data under a wide range of crystallographic and physical conditions.

This pipeline supports:
  -Diverse zone axes for diffraction simulation
  -Hydrostatic loading
  -Substitution
  -Defect introduction
  -Simulation of polycrystalline ring patterns
  -Application of Gaussian distribution for peak refinement and intensity profiles
  -Random in-plane rotational of 2D patterns
  -Adjustment of occupation factors

ADP is particularly useful for training and validating deep learning models, such as convolutional neural networks (CNNs), by enabling the creation of large, labeled datasets representing all seven crystal systems and 230 space groups. It helps address the scarcity of experimental diffraction data and improves classification performance under challenging conditions, such as unseen zone axes and structural distortions.

--------------------------------------------------------------------------------------------
## Files

### `ADP.py`

This is the main script. All other scripts in this repository were extracted or adapted from it.  
To use this code, you need to define three parameters:
1. `input_directory`: the folder containing your CIF files.
2. `output_directory`: the destination folder where generated patterns will be saved.
3. `(u1, v1, w1)`: the desired zone axis for 2D XRD pattern generation.

This script generates 2D XRD images in `.png` format for each CIF file in the output folder.

--------------------------------------------------------------------------------------------
### `ADP_1D_Gausssian_excel_output.py`

This script generates 1D XRD patterns with Gaussian-fitted intensity curves.  
To use it, define:
1. `input_directory`: folder containing CIF files.
2. `output_directory`: folder for saving the results.

Each output is an Excel file containing:
- Column 1: 2θ angle values from 0 to 180 degrees (step = 0.05°, adjustable).
- Column 2: intensity values computed using Gaussian fitting for each diffraction peak.

--------------------------------------------------------------------------------------------
### `ADP_1D_Only_Peaks_excel_output.py`

This script generates 1D XRD patterns using only peak intensities (no Gaussian fitting).  
You need to define:
1. `input_directory`
2. `output_directory`

The output Excel file contains:
- Column 1: 2θ angle values (0–180°, step 0.05°, adjustable).
- Column 2: raw peak intensity values at corresponding angles.

--------------------------------------------------------------------------------------------
### `ADP_Gaussian_2D_3D.py`

This script generates 2D XRD patterns by applying Gaussian distribution to intensity profiles. It first constructs a 3D Gaussian surface and then extracts the top view as the 2D XRD pattern.

Required parameters:
1. `input_directory`
2. `output_directory`
3. `(u1, v1, w1)`: target zone axis.

It generates `.png` images of both 3D and 2D Gaussian XRD patterns for each CIF.

--------------------------------------------------------------------------------------------
### `ADP_Hydrostatic_deformation.py`

This script simulates hydrostatic strain on crystal structures and generates corresponding 2D XRD patterns.

Required parameters:
1. `input_directory`
2. `output_directory`
3. `(u1, v1, w1)`: target zone axis.
4. `Hydro`: percentage of hydrostatic loading.  
   - `Hydro = 1.1` means +10% lattice expansion.  
   - `Hydro = 0.8` means −20% compression.

Each CIF's unit cell is scaled accordingly, and 2D XRD patterns are saved as `.png` files.

--------------------------------------------------------------------------------------------
### `ADP_Removing_atoms_NonBCC_to_BCC.py`

This script simulates atomic defects by removing atoms while preserving the BCC lattice framework.

Parameters:
1. `input_directory`
2. `output_directory`
3. `(u1, v1, w1)`
4. `defect`: fraction of atoms to remove (e.g., `0.1` for 10%, `0.8` for 80%).

The code retains atoms at fractional coordinates (0, 0, 0) and (0.5, 0.5, 0.5), ensuring the final configuration resembles a BCC structure. The result is a `.png` 2D XRD image per CIF.

--------------------------------------------------------------------------------------------
### `ADP_Replacing_Atoms.py`

This script simulates atom substitution by randomly replacing atoms in the unit cell with others from the periodic table.

Parameters:
1. `input_directory`
2. `output_directory`
3. `(u1, v1, w1)`
4. `repp`: replacement percentage (e.g., `0.01` = 1%, `0.4` = 40%).

The output includes `.png` 2D XRD patterns with altered atomic configurations.

--------------------------------------------------------------------------------------------
### `ADP_Ring_gausssian.py`

Polycrystalline materials exhibit ring-shaped 2D XRD patterns due to their random orientations.  
This script simulates such patterns.

Parameters:
1. `input_directory`
2. `output_directory`

It generates `.png` images of ring-like 2D XRD patterns per CIF.

--------------------------------------------------------------------------------------------
### `ADP_occupation_factor.py`

This script applies element-specific occupation factors from each CIF file and generates corresponding 2D XRD patterns.

Parameters:
1. `input_directory`
2. `output_directory`
3. `(u1, v1, w1)`

It reads each CIF, modifies the occupation factor per atom, and generates a `.png` image per pattern.

--------------------------------------------------------------------------------------------
### `ADP_random_angle_rotation.py`

This script rotates 2D XRD patterns by random in-plane angles around the diffraction center.

Parameters:
1. `input_directory`
2. `output_directory`
3. `(u1, v1, w1)`

For each CIF, a randomly rotated 2D XRD `.png` image is generated to simulate orientation variance.

--------------------------------------------------------------------------------------------
## Author

Ayoub Shahnazari  
University of Rochester  
Advisor: Professor Niaz Abdolrahim
