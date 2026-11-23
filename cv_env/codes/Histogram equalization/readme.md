What it does

It redistributes brightness so every gray level gets used about equally. Contrast stretching pulls the whole range wider with one straight-line formula. Equalization is smarter: it gives more room to brightness values with lots of pixels and squeezes the ones with few.

The problem it solves

Say a dark X-ray has 90% of its pixels between 20 and 60. All the detail is crammed into 40 gray levels, and your eyes can't separate them. Stretching helps, but if you have one bright outlier, it barely works. Equalization looks at where the pixels actually are and spreads that crowd apart, so the detail becomes visible.

The logic (the part that confuses everyone)

The question is: how do I decide how far apart to push each brightness level?

Answer: use the running total of pixels (the CDF). Where many pixels sit, the running total climbs fast, so those levels get pushed far apart. Where few pixels sit, it barely moves, so those levels get squashed together.

new_value = CDF(old_value) * 255

Tiny example, 10 pixels: five are 100, three are 110, two are 120.

Running total at 100 is 50%, so new = 0.5 * 255 ≈ 128
Running total at 110 is 80%, so new = 0.8 * 255 ≈ 204
Running total at 120 is 100%, so new = 1.0 * 255 = 255

Three values that were 10 apart are now 128, 204, 255, far apart and easy to see. The most crowded level (100) got the biggest chunk of new space. That's the whole algorithm.

Notice the darkest pixel became 128, not 0. That's the exact reason OpenCV subtracts the smallest CDF value, which I mentioned in the gotchas.

Equalization vs stretching

	Stretching	Equalization
Mapping	straight line	based on the actual histogram
Hurt by outliers	yes	much less
Result	histogram keeps its shape	histogram becomes roughly flat

Where it's used in industry

Medical imaging: dark X-rays, CT, and mammograms, so faint tissue becomes visible.
Satellite and aerial imagery: hazy or low-contrast terrain gets its detail back.
Face recognition and security cameras: lighting varies wildly, so images are equalized first to make faces comparable.
Microscopy: low-contrast cells become countable.
Underwater and night vision images: both are dull and low contrast by nature.
Preprocessing for ML and OCR: a consistent brightness distribution makes later steps behave better.