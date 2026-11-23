What it does

It flips every pixel's brightness: black becomes white, white becomes black, dark gray becomes light gray. It's the same as an old camera film negative.

The logic

A grayscale pixel is a number from 0 (black) to 255 (white). The negative just does:

new_pixel = 255 - old_pixel

Examples:

0 (black) → 255 (white)
255 (white) → 0 (black)
200 (bright) → 55 (dark)
128 (mid gray) → 127 (mid gray, basically unchanged)

That's the whole algorithm. Every pixel gets flipped around the middle.

Why anyone uses it

Your eyes are bad at spotting small bright or gray details inside a big black area. Flip the image and the same details sit on a white background, where they're much easier to see. This is why it's used in medical images (X-rays, mammograms), where a small bright spot can be hard to notice against a huge dark background. Your textbook will say this as "enhancing gray or white detail embedded in dark regions.