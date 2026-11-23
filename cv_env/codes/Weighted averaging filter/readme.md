What it does

Same sliding window as the average filter, but the pixels don't all get an equal vote. The center pixel counts the most, and the farther a neighbor is, the less it counts.

The kernel

1  2  1
2  4  2   ÷ 16
1  2  1
Center: 4 votes
Side neighbors: 2 votes each
Corners: 1 vote each
Total: 4 + 4×2 + 4×1 = 16, which is why we divide by 16

Tiny example

10  10  10
10 [90] 10
10  10  10
Plain average: (8×10 + 90) / 9 = 18.9
Weighted: (4×90 + 2×40 + 1×40) / 16... let me do it cleanly. Center = 4×90 = 360. Four sides = 4×(2×10) = 80. Four corners = 4×(1×10) = 40. Total = 480, divided by 16 = 30

The weighted filter keeps the center's identity more (30 vs 19), so it blurs less. That is the whole idea.

The problem it solves

The plain average treats a far corner neighbor the same as the pixel right beside you, which is unfair, because nearby pixels are more related to you. Weighted averaging respects distance. You get noise reduction with less smudging of edges and detail.

Averaging vs weighted

	Average	Weighted
Neighbor votes	equal	closer = bigger
Blur	stronger	gentler
Edges	smeared more	preserved a bit better

Where it's used

This kernel is a tiny version of the Gaussian filter, one of the most-used filters in vision.

Noise reduction before edge detection: Canny edge detection starts with a Gaussian blur.
Photo apps: soft-focus and portrait smoothing.
Image pyramids and downscaling: blur first so the shrunken image doesn't get jagged.
Preprocessing for ML and OCR.