What it does

It turns a grayscale image into pure black and white. You pick a cutoff number T (the threshold):

if pixel > T  →  255 (white)
else          →  0 (black)

With T = 127:

200 → 255
130 → 255
100 → 0
30 → 0

No in-between shades survive. Every pixel is forced to make a choice.

Why people use it (the problem it solves)

Computers are bad at "what is this image about?", but great at "is this pixel part of the thing I care about, yes or no?" Thresholding answers that yes/no. It separates object from background, and once you have that, everything else gets easy: count the objects, measure their size, find their edges, read the text.

Where it's used in industry

Document scanning and OCR: turning a photo of a page into clean black text on white, before reading the letters.
Factory inspection: a camera checks a PCB or bottle cap. Defects show up as dark blobs, and threshold isolates them.
Medical imaging: separating a bright bone or tumor region from tissue as a first step.
Barcode/QR scanners and number plate readers: same idea, binarize first.
Cell counting in microscopy: cells become white blobs, then you count blobs.

Is it useful? Honest answer

As a building block, very. As a standalone solution, weak. A single fixed T only works when lighting is even. If one corner of your photo is in shadow, that whole corner goes black, and no value of T fixes it. That's why the real world uses Otsu's method (it picks T automatically from the histogram) and adaptive thresholding (a different T for each local region). For your lab, basic global thresholding is the topic, but mention in your report that it fails under uneven lighting. That sentence alone makes your report look like you understood it.