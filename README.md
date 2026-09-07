# Python for Astronomy

Introductory Python workshops for Astronomy MSc students, University of Leeds, 2026-2027.

## Workshops

Work through the notebooks in order:

1. [Getting started](Workshop_0_Getting_Started.ipynb): installation with pip or conda on Linux/macOS, Jupyter, Python basics, arrays, functions, plotting and debugging.
2. [FITS files and plotting](Workshop_1_FITS_and_Plotting.ipynb): inspect astronomical images and metadata, choose display scaling, use celestial coordinates and save figures.
3. [Units and coordinates](Workshop_2_Units_and_Coordinates.ipynb): physical quantities, coordinate transformations, angular separations and catalogue matching.
4. [Modelling observations](Workshop_3_Modelling_Observations.ipynb): synthetic observations, sinusoidal fitting, residuals, period searches and phase folding.

## Getting started

Download this repository using **Code → Download ZIP** and extract it, or clone it with Git:

```bash
git clone https://github.com/johnilee/PythonForAstro.git
cd PythonForAstro
```

Read the installation section of **Workshop 0** in GitHub's notebook preview before launching Jupyter. It provides complete pip and conda instructions for NumPy, Matplotlib, Astropy, SciPy, JupyterLab and ipykernel.

Launch JupyterLab from the repository folder with your workshop environment activated:

```bash
python -m jupyterlab
```

Keep the notebooks alongside the `data/` and `images/` folders so that relative paths work. Run cells in order and attempt the exercises. Before sharing completed work, restart the kernel and run all cells to check reproducibility.

## Data and images

The FITS files used in Workshop 1 are included in `data/`. Supporting illustrations are in `images/`; source acknowledgements appear in the notebooks and FITS metadata. Please retain these acknowledgements when reusing those materials.
