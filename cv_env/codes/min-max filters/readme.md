What they do

Same sliding window again, but now:

Min filter: new pixel = the smallest of the 9 values
Max filter: new pixel = the largest of the 9 values

Tiny example

10  10  10
10 [255] 10      min → 10 (white speck gone)    max → 255 (speck spreads)
10  10  10

200 200 200
200 [0] 200      min → 0 (black speck spreads)   max → 200 (black speck gone)
200 200 200

The problem each one solves

Min filter removes salt noise (bright specks), because a bright value never wins a "smallest" contest.
Max filter removes pepper noise (dark specks), because a dark value never wins a "largest" contest.

Each one fixes one kind of noise and makes the other kind worse. Median fixed both, which is why it's the usual choice. Min and max are more specialised.

What they do to the whole image

Min: bright regions shrink, dark regions grow. The image gets darker.
Max: bright regions grow, dark regions shrink. The image gets brighter.

Where it's used

Removing one kind of noise when you know it's only salt or only pepper
Finding the brightest or darkest points in a region (the max filter is a quick way to find local peaks)
Morphology: min = erosion, max = dilation. These are the base of shape processing in OCR, fingerprint cleanup, and defect detection in factories. Remove small blobs with erosion, fill small holes with dilation.
Shadow and highlight cleanup in document scanning