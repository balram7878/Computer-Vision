What it is

Sobel measured how fast brightness changes (first derivative). The Laplacian measures how fast that change itself changes (second derivative). Remember, "derivative" just means difference between neighbors, so second derivative = difference of the differences.

See it on one row of pixels

pixels:        10   10   10  200  200  200
1st diff:         0    0  190    0    0       ← Sobel-style: one big spike at the edge
2nd diff:           0  190 -190    0         ← Laplacian: a positive-negative pair
Flat area: 0
Edge: a positive value on one side and a negative value on the other, with a zero crossing right at the edge

So the Laplacian responds to the start and end of a brightness change, not the change itself. That's why its edges are thin.

The kernel

 0   1   0
 1  -4   1
 0   1   0

It means: add the 4 neighbors, subtract 4 times the center. Basically "how different is this pixel from the average of its neighbors?"

Check with a speck:

10  10  10
10 [90] 10      →  (10+10+10+10) - 4×90 = -320
10  10  10

A big value, because the center disagrees with its neighbors. On a flat area it's 40 - 40 = 0. The kernel values sum to 0, same reason Sobel gave 0 on flat regions.

What it does to the image

The output is mostly black (flat areas = 0) with bright thin outlines on edges, corners, lines, and tiny details. It's a detail map, like Sobel's magnitude but thinner and sharper. It also lights up every noise speck, because a speck is an extreme local difference.

Sobel vs Laplacian

	Sobel (1st order)	Laplacian (2nd order)
Measures	change	change of the change
Edges	thick, strong	thin, fine
Direction	separate Gx and Gy	one kernel, all directions
Noise	sensitive	much more sensitive
Fine detail, points, thin lines	weaker	stronger

Where it's used

Image sharpening: the main use, and your next topic. Add the Laplacian back to the original and edges get boosted.
Blur detection: the variance of the Laplacian is the standard trick to check whether a photo is sharp or blurry (low variance = blurry). Used in phone cameras, document scanners, and autofocus.
Edge and blob detection: LoG (Laplacian of Gaussian) is a classic for finding edges and spots.
Medical imaging: bringing out fine structures in X-rays and microscopy.
Defect detection: tiny scratches and cracks show up as bright thin lines.