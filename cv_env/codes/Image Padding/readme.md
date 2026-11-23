Point operation: new pixel = f(old pixel)
Filter: new pixel = f(old pixel + its neighbors)

And that's why contrast stretching can't kill a noise speck: it sees a lone 255, has no idea everything around it is 10, and stretches it like any other 255. A filter looks around, sees the 10s, and can say "this one doesn't belong."

Now padding, the first thing every filter needs.

The problem it solves

A 3x3 window needs 8 neighbors around the center pixel. Take the top-left corner pixel: it has no pixels above it and none to its left. The window hangs off the edge of the image, and there's nothing to read.

 ?  ?  ?
 ?  [5] 8  ...
 ?  2  9

Three options: skip the border pixels (image shrinks, you lose data), crash, or add fake pixels around the border so the window always has something to read. That last one is padding.

The common padding types

Take a tiny 3x3 image and pad 1 pixel on each side:

Original:
 1  2  3
 4  5  6
 7  8  9

Zero padding: fill the border with 0.

 0  0  0  0  0
 0  1  2  3  0
 0  4  5  6  0
 0  7  8  9  0
 0  0  0  0  0

Replicate padding: copy the nearest edge pixel outward.

 1  1  2  3  3
 1  1  2  3  3
 4  4  5  6  6
 7  7  8  9  9
 7  7  8  9  9

Reflect padding: mirror the image across the edge.

 5  4  5  6  5
 2  1  2  3  2
 5  4  5  6  5
 8  7  8  9  8
 5  4  5  6  5

Which one is used when

Zero: simplest, but creates a dark frame around blurred images, because the average pulls toward 0 at the borders.
Replicate / reflect: look more natural, no dark frame. Better for real results.