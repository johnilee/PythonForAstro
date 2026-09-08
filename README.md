# Python for Astronomy

Introductory Python workshops for Astronomy MSc students, University of Leeds, 2026-2027.

## Workshops

Work through the notebooks in order:

1. [Getting started](Workshop_0_Getting_Started.ipynb): Jupyter, Python basics, arrays, functions, plotting and debugging.
2. [FITS files and plotting](Workshop_1_FITS_and_Plotting.ipynb): inspect astronomical images and metadata, choose display scaling, use celestial coordinates and save figures.
3. [Units and coordinates](Workshop_2_Units_and_Coordinates.ipynb): physical quantities, coordinate transformations, angular separations and catalogue matching.
4. [Modelling observations](Workshop_3_Modelling_Observations.ipynb): synthetic observations, sinusoidal fitting, residuals, period searches and phase folding.

## Getting started

### Load the Python environment

It is assumed you are familiar with the Linux/Unix operating system and terminal environment.  If not, please revisit the [Linux/Unix tutorial](https://johnilee.github.io/UnixTutorial) before starting.

On the Linux machines in Bragg 4.04, open a terminal and run:

```bash
module load maps-condaenv
```

This makes the workshop Python environment available in that terminal. Run it at the start of each new terminal session. No package installation or environment creation is needed.

A **Python environment** contains a Python interpreter and its installed packages. Check the Python made available by the module with these terminal commands:

```bash
python -c "import sys; print(sys.executable)"
python -c "import numpy, matplotlib, astropy, scipy, jupyterlab, ipykernel; print('All required packages are available.')"
```

The first command displays the Python executable's path. The second checks the packages needed for all four workshops. If an import fails, note the missing package and ask the demonstrator for help.

| Package | Purpose |
| --- | --- |
| NumPy | Numerical arrays and calculations |
| Matplotlib | Figures and image display |
| Astropy | FITS files, units, coordinates and period searches |
| SciPy | Curve fitting and catalogue-matching support |
| JupyterLab | The browser interface used to open notebooks |
| ipykernel | Runs Python code for Jupyter |

`pathlib` and `sys`, used in the workshops, come with Python.

**Run these commands in the terminal, not in a Python code cell.**

### Download this repository

To effectively run the workshop scripts you'll need to download the files to your workstation from this GitHub repository (or repo).  Replace `YOUR_USERNAME` below with your university username, then create a directory on the machine’s local storage and clone the repo:

```bash
mkdir -p /local/data/YOUR_USERNAME
cd /local/data/YOUR_USERNAME
git clone https://github.com/johnilee/PythonForAstro.git 
```

This will create a new directory called `PythonForAstro/` filled with the contents of this repo.  Keep the notebooks alongside the `data/` and `images/` folders. In the same terminal, change into this folder and start JupyterLab:

```bash
cd PythonForAstro
python -m jupyterlab
```

Open `Workshop_0_Getting_Started.ipynb` from JupyterLab's file browser. Keep the terminal running while you work. Follow the demonstrator's instructions for opening JupyterLab in your browser if needed.

## Data and images

The FITS files used in Workshop 1 are included in `data/`. Supporting illustrations are in `images/`; source acknowledgements appear in the notebooks and FITS metadata. Please retain these acknowledgements when reusing those materials.
