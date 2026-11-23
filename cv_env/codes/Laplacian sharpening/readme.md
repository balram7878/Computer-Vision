The Laplacian gives you a map of the edges, but you don't want just an edge map, you want the original photo, but crisper. So you add the edge map back onto the original.

The logic

sharpened = original - Laplacian      (for the kernel with -4 in the center)

Back to our single row of pixels:

pixels:      10   10   10  200  200  200
Laplacian:    0    0  190 -190    0    0     (at the two edge pixels)
original - Laplacian:
             10   10 -180  390  200  200
clip 0-255:  10   10    0  255  200  200

The dark pixel next to the edge got darker (10 → 0), and the bright pixel got brighter (200 → 255). The step between dark and bright is now bigger, so your eye reads the edge as crisper. Flat areas are untouched, since adding 0 changes nothing.

One-kernel version

Subtracting the Laplacian from the original can be folded into one kernel:

 0  -1   0
-1   5  -1
 0  -1   0

This is just "identity minus Laplacian": the center is 1 - (-4) = 5. Same result, one pass.

Where it's used

Photo editing: the "sharpen" slider in phone and photo apps
Medical imaging: making fine structures in X-rays and scans easier to see
Document scanning and OCR: crisper text edges
Satellite and aerial images: bringing out roads and boundaries
Fixing slightly soft or blurry photos from camera shake or bad focus