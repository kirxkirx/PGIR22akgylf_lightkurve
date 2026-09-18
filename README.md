# TESS Photometry Analysis of Nova PGIR22akgylf with Lightkurve

This repository contains Jupyter notebooks for analyzing TESS (Transiting Exoplanet Survey Satellite) photometry of classical nova PGIR22akgylf during its eruption in 2022. The analysis focuses on detecting and validating periodic brightness variations during the nova's rise to maximum light.

## Overview

Nova PGIR22akgylf erupted on 2022-08-16 and was captured by TESS during Sector 55. Our analysis reveals an unexpected 0.1802-day periodic modulation in the nova's lightcurve as it brightened toward its peak - a phenomenon rarely observed in classical novae.

## Notebooks

### 1. [Square Aperture Photometry Analysis](PGIR22akgylf_lk_square_aperture.ipynb)
**Primary lightcurve extraction and period analysis using square apertures**

- Extracts TESS Sector 55 lightcurves using 3×3 pixel square apertures
- Analyzes the full sector and splits into pre-eruption/eruption halves  
- Compares nova lightcurve with nearby check stars
- Performs Lomb-Scargle period search revealing 0.1802d periodicity
- Extends analysis to all available TESS sectors (14, 15, 54, 55, 74, 75, 81, 82)
- Implements background subtraction and detrending methodology

### 2. [Circular Aperture Photometry Analysis](PGIR22akgylf_lk_circular_aperture.ipynb)  
** !!! THIS NOTEBOK IS INCOMPLETE !!! **
**Optimized photometry using circular apertures with systematic parameter testing**

- Tests multiple circular aperture radii (1.5, 2.0, 2.5 pixels)
- Uses ring-shaped background regions with various inner/outer radii
- Selects optimal aperture configuration based on Median Absolute Deviation

### 3. [Individual Pixel Analysis](PGIR22akgylf_lk_individual_pixel_lightcurves.ipynb)
**Per-pixel periodogram analysis to spatially localize periodic signals**

- Constructs lightcurves and periodograms for each individual pixel
- Creates period and power maps showing spatial distribution of signals
- Validates that 0.1802d signal originates from nova position
- Distinguishes nova periodicity from nearby eclipsing binary (0.1991d)
- Demonstrates background subtraction effectiveness in removing instrumental signals

### 4. [Lightcurve simulation](PGIR22akgylf_simulations.ipynb)
**Simulation-based validation of the period detection methodology**

- Tests pipeline reliability using controlled synthetic signals
- Combines real nova trend with known 0.200d periodic signal
- Validates that complex lightcurve evolution doesn't affect period detection accuracy
- Demonstrates <0.1% period recovery error even with authentic nova complexity
- Provides confidence in detected periodicities through end-to-end testing

### 5. [Sectors 74 and 75 matched-cadence period search](PGIR22akgylf_sectors74_75_period_search.ipynb)
**Post-eruption search for the 0.1802-day signal and its 0.3604-day double period**

- Bins the native 200-second Sector 74 and 75 data to the 10-minute Sector 55 cadence
- Repeats the Sector 55 clipping, detrending, background, and Lomb-Scargle diagnostics
- Measures the nearby eclipsing binary through a separate proxy aperture
- Removes a harmonic model of the eclipsing-binary leakage before repeating the search
- Tests both sectors separately and together at fixed periods of 0.1802 and 0.3604 days

## Key Findings

- **Periodic Modulation**: Clear 0.1802-day periodicity detected during nova's rise to maximum
- **Spatial Localization**: Period analysis confirms signal originates from nova position
- **Temporal Evolution**: Modulation present only during eruption phase (Sector 55)
- **Background Separation**: Successfully distinguishes nova signal from nearby variable star contamination
- **Methodology Validation**: Simulation tests confirm robust period detection capabilities

## Requirements

- Python 3.7+
- `lightkurve` - TESS data analysis
- `numpy` - Numerical computations  
- `matplotlib` - Plotting and visualization
- `scipy` - Signal processing (Savitzky-Golay filtering, curve fitting)
- `astropy` - Astronomical data handling
- `photutils` - Aperture photometry
- `tqdm` - Progress bars

## Starting the notebook environment

The virtual environment is already set up in `.venv`. From a terminal, change to this repository, activate the environment, and start Jupyter Notebook:

```bash
cd /home/kirx/current_work/PGIR/rerun_lk/PGIR22akgylf_lightkurve
source .venv/bin/activate
python -m notebook
```

Jupyter Notebook will open in your web browser. Open any `.ipynb` file and select the **Python (PGIR22akgylf)** kernel if Jupyter asks you to choose one. Stop the notebook server by pressing `Ctrl+C` in the terminal. When finished, leave the virtual environment with:

```bash
deactivate
```

## Recreating the environment

To rebuild the environment later, run these commands from the repository directory:

```bash
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements-notebooks.txt
python -m ipykernel install --prefix .venv --name pgir22akgylf --display-name "Python (PGIR22akgylf)"
```

The notebooks fetch TESS data from MAST, so running their analysis cells requires an internet connection.

## Usage

The notebooks can be executed independently. Start with the square aperture analysis for the primary Sector 55 results. Use the Sectors 74 and 75 notebook for the focused post-eruption comparison.

## Data Sources

- **TESS Full-Frame Images**: Retrieved via the `lightkurve` package
- **Quality Filtering**: Applied 'hard' quality cuts to remove problematic data
- **Time Coverage**: Primary analysis focuses on TESS Sector 55 (2022-08-05 to 2022-09-01)

## Citation

If you use this analysis in your research, please cite the associated publication
(once it's out) and acknowledge the TESS mission and data archive.
