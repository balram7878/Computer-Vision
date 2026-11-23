What it does

Clipping sets a floor and a ceiling for pixel values. Anything below the floor gets raised to the floor, anything above the ceiling gets lowered to the ceiling, and everything in between stays untouched.

With low = 50 and high = 200:

20 → 50
50 → 50
120 → 120 (unchanged)
230 → 200

Thresholding vs clipping

Thresholding destroys all shades (everything becomes 0 or 255). Clipping keeps the middle shades and only chops the extremes.

The problem it solves

Sometimes the extreme values are garbage, or you just don't care about them: blown-out highlights, sensor noise in the darkest areas, a few crazy-bright outlier pixels. Clipping removes them so the useful range is what's left. It's also used to keep values inside 0 to 255 after other operations.

Where it's used in industry

Medical imaging (CT/X-ray): "windowing" clips intensities to a range so the radiologist sees only lung tissue or only bone.
Satellite and aerial imagery: clouds and glare are super bright and ruin contrast. Clip the top 2% and the land becomes visible.
Camera pipelines: handling overexposed highlights and keeping values valid after brightness or gain changes.
Machine learning preprocessing: clip outlier pixel values before normalizing so one bright speck doesn't wreck the scale.

Images to download

Your X-ray (reuse it): clip to something like 80-180 to see the mid-tone detail
An overexposed photo: a bright sky or window glare, to show the highlights being chopped
A dark or underexposed photo: the low end gets clipped
A satellite image with clouds: the most "real world" example in the set