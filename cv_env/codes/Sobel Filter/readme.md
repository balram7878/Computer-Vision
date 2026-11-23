The idea: an edge is a sudden jump

A "derivative" here is just the difference between neighboring pixels. No calculus.

pixels:      10  10  10  200  200  200
difference:     0   0  190    0    0

Flat areas give 0. At the dark-to-bright jump you get a huge number. Big difference = edge. That's the whole idea of first-order derivative.

What Sobel does

It measures that difference with a 3x3 kernel, in two directions:

Gx (finds vertical edges)     Gy (finds horizontal edges)
-1  0  +1                     -1  -2  -1
-2  0  +2                      0   0   0
-1  0  +1                     +1  +2  +1

Gx = "right side minus left side". On a flat area the left and right cancel to 0. At an edge they don't, so you get a big value. The 2s in the middle row are the weighted-averaging idea again: the center row counts more, which also smooths a bit of noise. Gy does the same top minus bottom.

Then combine both:

edge strength = sqrt(Gx² + Gy²)

Where it's used

Edge detection as the first step in object detection and shape finding
Lane detection in self-driving and driver-assist systems
Document scanning: finding the page borders
Medical imaging: outlining bones, organs, and tumors
Factory inspection: measuring part edges and finding cracks
Canny edge detection (a famous algorithm) uses Sobel inside it