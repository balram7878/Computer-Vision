What it does

Every pixel is stored as 8 bits. Bit-plane slicing splits the image into 8 separate black and white images, one per bit position. Plane 7 holds the leftmost bit of every pixel, plane 0 holds the rightmost.

Take a pixel with value 200:

200 = 128 + 64 + 8 = 1 1 0 0 1 0 0 0
bit:                 7 6 5 4 3 2 1 0

Pixel 200 contributes a 1 to planes 7, 6, and 3, and a 0 to the rest.

The problem it solves

You want to know: which bits actually carry the picture, and which are just junk? The bits aren't equal:

Bit 7 is worth 128, so flipping it changes the pixel massively.
Bit 0 is worth 1, so flipping it changes nothing your eye can see.

So the top planes (7, 6, 5) hold the shape and structure, and the bottom planes (2, 1, 0) look like random noise. Slicing lets you prove this visually.

The logic

plane k = (pixel >> k) & 1

>> k shifts the bits right so bit k lands in the last position, and & 1 keeps only that bit.

You can also rebuild the image:

image = sum of (plane k × 2^k)  for k = 0 to 7

If you rebuild using only the top 2 or 4 planes, you still recognize the picture. That's the whole insight.

Where it's used in industry

Image compression: the top planes carry the information, so storing fewer low bits saves space with barely visible loss. This is the same idea as the quantization from topic 2, so it connects.
Steganography and watermarking: hide a secret message in plane 0 (LSB). Changing it alters each pixel by at most 1, so nobody can see it.
Forensics and tamper detection: edited images often show broken patterns in the low planes.
Medical image transmission: send the top planes first for a quick preview, then the rest.
Image analysis: checking how many bits of an image are meaningful versus sensor noise.

Honest take: it's mostly a teaching and analysis tool. You rarely use it to "improve" an image. Its value is the understanding of bit importance, plus the LSB hiding trick. Say that in your report.

Images to use

Your X-ray: smooth tissue gradients, so the low planes turn to pure noise.
A detailed photo (cameraman or a building): shows structure surviving in the top planes.
A document or text image: the top planes look almost identical to a thresholded image, which is a nice link to topic 5.
A smooth gradient (sky, sunset): the low planes are noisy, and the high planes show big blobs.