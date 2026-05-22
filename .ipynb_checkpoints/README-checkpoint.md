# TypeIt_Data_Reduction_Pipeline
A data reduction pipeline written as part of my graduate work to clean telescope data and prepare it for spectral fitting. Output from 2D long-slit spectra is 3D data cubes (to work with LZIFU).

## Overview

This pipeline processes raw 2D FITS files from the DeVeny Spectrograph from the Lowell Discovery Telescope into cleaned, calibrated spectral data cubes ready for scientific analysis. It handles error frame propagation, wavelength calibration, and spectral extraction.

## Requirements

- Python 3.11.7
- Astropy 6.1.2
- NumPy 1.26.4
- SciPy 1.11.4
- Matplotlib 3.8.0

Install dependencies:
pip install astropy numpy scipy matplotlib jupyter

## Usage
I wrote this pipeline in a step-wise fashion. As such, it is broken up into four jupyter notebooks. 
The four notebooks run in the following order:

### Notebook 1 -  DeVeny Data Reduction Pipeline Data Prep
Notebook 1 prepares all the raw files for data reduction by:
    - Trimming overscan
    - Adding an error frame for calibration frames
    - Creating a master bias file (and subtracting it from each science and calibration frame)
    - Creating a master dome flat file
    - Creating a master arc file (for wavelength calibration)
    - Checking wavelength calibration (NOTE: wavelength calibration was done in a separate notebook by fitting gaussians to the master arc file and resulting in a text file labeled Wav_'+ date +'-2_' + setting + '.txt'. The example dataset includes this, but such file would be needed if not)
- **Edit required:** Cell 6 includes a many inputs for the target, observing date, file numbers, and exposure time. This is the only cell that needs to be changed, and will need to be changed in each notebook. 

### Notebook 2 - DeVeny Data Reduction Galaxy Reduction
Notebook 2 reduces the galaxy and standard star files to produce cleaned 2D FITS files:
    - Add error frames for the science galaxy/star data files
    - Divide each science frame by exposure time
    - Median-combine the science frames of each object (galaxy or standard star)
    - Dome divide (flat field) the science frames
    - Sky subtract the science frames to get rid of most sky emission lines.
    - Flux calibrate the galaxy based on the standard star frame and literature value
- **Edit required:** Same as notebook 1, change cell 6.

### Notebook 3 - Creating 3D Data Cube Unbinned
Notebook 3 was for the specific use of my datasets. In order to analyze the emission lines, I decided to use LZIFU, which takes 3D IFU data. In order to make my data work with LZIFU, I needed to transform the 2D dataset into a 3D data cube by adding a z-axis. This notebook is only needed in this specific use case. 
- **Edit required:** Same as notebook 1, change cell 3.

### Notebook 4 - Spatial Binning
Notebook 4 takes the 3D unbinned data cube produced by notebook 3 and produces 4 binned 3D data cubes. It finds the center of the galaxy and bins around that in 2-, 3-, 4-, and 5- pixel bins. This code was done to check if we could get stronger signal for some emission lines. 
- **Edit required:** Again, change cell 6. In this case, it only has half the inputs that the other three notebooks had. 

## Directory Structure

TypeIt_Data_Reduction_Pipeline/
├── v1.7 - DeVeny Data Reduction Pipeline Data Prep.ipynb
├── v2.7 - DeVeny Data Reduction Galaxy Reduction.ipynb
├── v3.7 - Creating 3D Data Cube Unbinned.ipynb
└── v4.7 - Spatial Binning.ipynb
├── Observations/
│   ├── Feb 16 2020/        # Input 2D FITS files for a specific observing date
│   ├── Wav_2-16_A.txt      # Initial wavelength calibration file
│   └── Wav_2-16_2_A.txt    # Gaussian fit to master arc emission lines, for a slightly more accurate wavelength calibration file
├── Working Files/          # Directory that houses many step-wise plots made using the reduction notebooks. Used to diagnose issues.
├── Standard Stars Accepted Flux Data/    # Directory included standard star data for stars used. Mainly taken from ESO and NAOJ sources
├── Galaxy Properties/                    # Mainly SDSS Information on each galaxy observed in this campaign
├── Binning Work/                         # spatial information from Ned Wright's cosmology calculator to figure out kpc scale for different                                                    binning scenarios from Notebook 4.
├── Flux Calibrated SPOGs/ #Output flux-calibrated 2D FITS files for galaxies from Notebook 2. 
├── 3D Output Cubes Unbinned/  #Output 3D FITS files for emission line analysis.
├── Binned 3D Output Cubes/    #Output Binned 3D FITS files for emission line analysis.
└── README.md

## Example Data

Example input files are provided in `Observations/` to test 
the pipeline and showcase its use.

## Output

- Processed data cubes saved to `3D Output Cubes Unbinned/` and `Binned 3D Output Cubes/`

## Background

This pipeline was developed as part of doctoral research at 
the University of Toledo studying shocked post-starburst galaxies.