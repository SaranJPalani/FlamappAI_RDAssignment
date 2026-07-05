# Curve Fitting Assignment

## What the assignment is asking

Provides a CSV file, `xy_data.csv` containing x and y coordinates of a curve in a random order and we are asked to find the value of the unknowns

The unknowns are:
- `θ` = the rotation angle
- `M` = the growth/decay factor inside the wave term
- `X` = the horizontal shift

## The equations

The curve can be written as:

$$
x = t \cos(\theta) - e^{Mt}\sin(0.3t)\sin(\theta) + X
$$

$$
y = 42 + t\sin(\theta) + e^{Mt}\sin(0.3t)\cos(\theta)
$$

The first is to undo the geometry first by subtracting the shift and unrotating the equations

After subtracting the shift and rotating backward:

$$
x - X = \cos(\theta)u - \sin(\theta)v
$$

$$
y - 42 = \sin(\theta)u + \cos(\theta)v
$$

Here, `u` behaves like the forward motion of the curve and `v` behaves like the wave part:

$$
u = t
$$

$$
v = e^{Mu}\sin(0.3u)
$$

## Method used in the notebook

1. Load the points from `xy_data.csv`.
2. Try a range of values for `θ` and `X`, then keep the pair that fits best.
3. For each pair, shift the data by `X` and `42`, then rotate the points backward.
4. Read the transformed coordinates as `u` for forward motion and `v` for the wave term.
5. Estimate `M` from the transformed wave values.
6. Print a small residual sample from the transformed points and also compute a uniform-sample L1 score by taking the mean absolute error with 500 points.
7. Check a smaller window around that result to make sure it is stable.

## Why this works

Reduce the main equations by undoing the rotation and shift to get a simple rotation curve.

Once the rotation and shift are removed the curve becomes much easier to interpret. The notebook can then test candidate `θ` and `X` values directly from the data, back out `u` and `v` and choose the pair that gives the smallest transformed error.

## Result from the notebook

The notebook predicts:

- `θ = 30.00000000`
- `X = 55.00000000`
- `M = 0.0299999897`


## Desmos section

The Desmos graph is the visual check for the same method.

In the screenshot, I used:

- `a = 0.5236` radians, which is 30°
- `X = 55`
- `M = 0.0299999897`

![Desmos screenshot](image.png)

After shifting by `X` and `42`, then rotating the points backward by `a`, the transformed points line up with the wave model very closely. That is why the Desmos graph supports the same final answer as the notebook.

## Citation

- Wikipedia, "Reversing a 2D Rotation matrix": https://en.wikipedia.org/wiki/Rotation_matrix

## Files

- `assignment_solution.ipynb` = the main notebook with the fitting process
- `xy_data.csv` = the data points
