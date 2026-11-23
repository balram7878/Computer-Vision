What it does

It takes an image whose brightness is squeezed into a narrow range and stretches that range to fill the full 0 to 255. Dull and washed out becomes punchy.

The problem it solves

Say a foggy photo has pixels only between 100 and 150. Nothing is truly black, nothing is truly white, so everything looks like gray soup. Your eyes can't separate 120 from 125, but they can easily separate 30 from 200. So you spread the values out.

The logic

Find the darkest pixel (rmin) and the brightest (rmax), then map them to 0 and 255 with a straight line:

s = (r - rmin) / (rmax - rmin) * 255

With rmin = 100 and rmax = 150:

100 → 0
125 → 127.5, so about 128
150 → 255

The darkest pixel becomes pure black, the brightest becomes pure white, and everything else is spread proportionally in between.

Clipping vs stretching

Clipping chops the extremes and leaves the middle untouched. Stretching chops nothing, it remaps every pixel so the whole range gets used.

Where it's used

Medical imaging: dim X-rays, CT, and MRI scans, so faint structures become visible
Satellite and aerial photos: hazy scenes get their detail back
Microscopy: low-contrast cells become easier to see and count
Camera auto-contrast and photo editors: the "auto levels" button is basically this
Preprocessing before thresholding or ML: a normalized range makes later steps behave consistently

Images to use

A foggy or hazy landscape
A dark, underexposed X-ray (not your already-good one)
A washed-out, faded old photograph
A low-contrast microscopy image

Check the histogram first. If it's already spread over 0 to 255, stretching will do nothing, and that makes a boring result.