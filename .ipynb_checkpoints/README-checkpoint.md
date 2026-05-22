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

The four notebooks run in the following order:

### Notebook 1 -  DeVeny Data Reduction Pipeline Data Prep
Brief description of what it does.
- **Edit required:** Change `filename` variable in cell 2 to your input file path.

### Notebook 2 - DeVeny Data Reduction Galaxy Reduction
Brief description.
- **Edit required:** Change `target_name` variable in cell 1.

### Notebook 3 - Creating 3D Data Cube Unbinned
Brief description.
- **Edit required:** Change `output_path` variable in cell 1.

### Notebook 4 - Spatial Binning
Brief description.
- **Edit required:** Change `final_output` variable in the last cell.

## Directory Structure

pipeline/
├── notebooks/
│   ├── 01_notebook_name.ipynb
│   ├── 02_notebook_name.ipynb
│   ├── 03_notebook_name.ipynb
│   └── 04_notebook_name.ipynb
├── data/
│   ├── 2d_files/        # Input 2D FITS files
│   └── output/          # Processed output files
├── example_data/
└── README.md

## Example Data

Example input files are provided in `example_data/` to test 
the pipeline before using your own observations.

## Output

- Processed data cubes saved to `output/`
- Input 2D files located in `2d_files/`

## Background

This pipeline was developed as part of doctoral research at 
[University] studying [brief description of science].