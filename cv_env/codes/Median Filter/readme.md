What it does

Collect the 9 pixels under the window, sort them, and pick the middle one (the 5th of 9). That value becomes the new pixel.

Tiny example

10  10  10
10 [255] 10
10  10  10

Sorted: 10, 10, 10, 10, 10, 10, 10, 10, 255. The middle (5th) value is 10.

Average gives (8×10 + 255) / 9 = 37, a gray smudge left behind
Median gives 10, the speck is completely gone

The problem it solves

Averaging uses every value, so one extreme pixel drags the result toward it. Median ignores extremes: a crazy value always sorts to the very end of the list, and the middle never picks it. This is why it's the standard fix for salt-and-pepper noise (random white and black specks).

Why it keeps edges sharper

On an edge, the window holds a mix of dark and bright pixels. Average blends them into a muddy gray. Median picks one of the real values, either dark or bright, so the edge stays a clean step.

Where it's used

Cleaning scanned documents and old photos with dust and specks
Sensor and transmission errors (dead pixels, corrupted data, bit errors)
Medical images and X-rays with isolated bright or dark artifacts
Preprocessing before thresholding or OCR, so specks don't become fake objects
Removing small unwanted dots in satellite or microscopy images