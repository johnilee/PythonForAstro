# Python syntax reference

Optional examples to revisit while working through the three workshops. The notebooks introduce the Python needed for their core tasks; this document supplies additional practice.

- [Workshop 1: Python basics, FITS and plotting](Workshop_1_FITS_and_Plotting.ipynb)
- [Workshop 2: Units, coordinates and catalogues](Workshop_2_Units_and_Coordinates.ipynb)
- [Workshop 3: Functions and modelling observations](Workshop_3_Modelling_Observations.ipynb)

Run the following setup before the examples in this document, then work through them in order:

```python
import numpy as np
import matplotlib.pyplot as plt

source_names = ["Star A", "Star B", "Star C"]
flux = np.array([0.98, 1.04, 1.10, 0.95, 1.03])

def calculate_count_rate(counts, exposure_seconds):
    return counts / exposure_seconds
```

## Arithmetic

Use `+`, `-`, `*`, `/` and `**` (powers). Parentheses control order. `//` is floor division and `%` is remainder; `^` is not exponentiation.

```python
print(3**2)
print((2 + 3) * 4)
print(7 // 2)
print(7 % 2)
```

## Lists, arrays and slices

A NumPy **array** supports numerical calculations over many measurements at once. Here each relative-flux value is a measured flux divided by a reference flux, so the values are dimensionless.

An **import** makes a package available in the kernel. `import numpy as np` gives NumPy the conventional short name `np`.

```python
import numpy as np

flux_list = [0.98, 1.04, 1.10, 0.95, 1.03]
flux = np.array(flux_list)

print("List repeated:", flux_list * 2)
print("Array multiplied:", flux * 2)
print("Shape:", flux.shape)
print("Data type:", flux.dtype)
print("Mean relative flux:", np.mean(flux))
```

Notice that multiplying a list repeats its contents, while multiplying a numerical array operates on each value. This element-by-element behaviour is called **vectorisation**.

`flux.shape` and `flux.dtype` are **attributes** containing information about the array. `np.mean(flux)` is a function call. `flux.mean()` is a **method**, a function accessed through an object, and gives the same mean.

### Slicing

A slice `values[start:stop]` includes `start` and excludes `stop`. Omitting a boundary means the beginning or end of the array. A third value gives the step.

```python
print("First value:", flux[0])
print("Indices 1 and 2:", flux[1:3])
print("First three:", flux[:3])
print("Every other value:", flux[::2])
```

### Two-dimensional arrays

An image is an array of rows and columns. Index it as `image[row, column]`, or equivalently `image[y, x]`. A slice alone does not change the image. However, NumPy slices normally share data with the original array: modifying a slice can modify the original. Use `.copy()` when you need an independent cutout.

```python
image = np.array([
    [10, 11, 12, 13],
    [20, 21, 22, 23],
    [30, 31, 32, 33],
])

ny, nx = image.shape  # unpack two values into two names
print("Rows:", ny, "Columns:", nx)
print("Row 1, column 2:", image[1, 2])
cutout = image[0:2, 1:3].copy()
print(cutout)
print("Cutout shape:", cutout.shape)
```

### Practice — predict an image slice

Before executing any code, predict the shape and contents of `image[1:3, :2]`. Then check your prediction.

Select the bottom-right pixel with negative indices. Which comes first in an image index: x or y?

## Line plots

### Make a labelled plot

Matplotlib separates the whole **figure** (`fig`) from the plotting **axes** (`ax`). `plt.subplots()` returns both objects, which we unpack into two names. Here each flux measurement corresponds to the time at the same array index.

We import Matplotlib’s plotting module as `plt` before using it.

```python
import matplotlib.pyplot as plt

time_days = np.array([0.0, 1.0, 2.5, 4.0, 6.0])

fig, ax = plt.subplots(figsize=(7, 4))
ax.plot(time_days, flux, marker="o", linestyle="none")
ax.set_xlabel("Time (days)")
ax.set_ylabel("Relative flux")
ax.set_title("Five observations of an example star")
plt.show()
```

`marker` and `linestyle` are keyword arguments controlling appearance. The axis labels explain what the numbers mean. Relative flux is dimensionless; the time axis needs a unit.

### Practice — modify the figure

Make another plot with a different marker colour and an informative title. Use `ax.axhline(1.0, color="gray", linestyle="--")` before `plt.show()` to mark the reference level.

Does changing the marker colour change any of the measurements?

## Compact syntax

**Argument unpacking:** a `*` before a sequence in a function call passes its elements as separate positional arguments. The parameter order must match the function definition.

```python
parameters = [1200, 30.0]
print(calculate_count_rate(*parameters))
print(calculate_count_rate(parameters[0], parameters[1]))
```

**List comprehensions:** a short way to build a list from repeated operations. The first two examples below produce the same result.

```python
squared_values = []
for value in [1, 2, 3]:
    squared_values.append(value**2)

squared_compact = [value**2 for value in [1, 2, 3]]
print(squared_values)
print(squared_compact)
```

**Useful iteration patterns:** `range(n)` supplies integers from 0 through `n - 1`. `zip()` pairs entries from sequences; use matching lengths when each name should correspond to a measurement.

```python
for i in range(len(source_names)):
    print(i, source_names[i])

source_fluxes = np.array([0.98, 1.04, 1.10])
for name, value in zip(source_names, source_fluxes):
    print(name, value)
```

**Keyword/value pairs:** a dictionary maps keys to values. FITS headers behave similarly when you look up metadata in Workshop 1. `.get()` can supply a fallback for a missing key.

```python
metadata = {"target": "Example star", "exposure_seconds": 30.0}
print(metadata["target"])
print(metadata.get("filter", "Not recorded"))
```

**Sampling and missing values:** `np.linspace(start, stop, number)` makes an evenly spaced array, including both endpoints by default. `np.nan` represents a missing or invalid numerical value; it is not zero.

```python
model_times = np.linspace(0, 2, 5)
print(model_times)

incomplete_flux = np.array([1.0, np.nan, 1.2])
print("Ordinary mean:", np.mean(incomplete_flux))
print("Mean ignoring NaNs:", np.nanmean(incomplete_flux))
```

Ignoring missing measurements can be useful, but investigate why they are missing. Workshop 1 uses `np.nan...` functions when inspecting an image.

## Help and debugging

Use `help(np.mean)` to inspect a function's inputs, result and examples. Read a traceback from its final line, then locate the indicated instruction. Restart the kernel and run all cells before sharing a notebook; saved output does not establish that the current code runs in order.
