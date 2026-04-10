entropy
Description: Computes the Shannon entropy of a grayscale image, measuring its randomness or information content. Entropy is higher for complex, textured images and zero for a completely uniform image
.
Purpose: Use entropy to quantify how much information or variation is in an image. This is useful for comparing compression levels, texture analysis, or any situation where image complexity matters.
Syntax:
scilab
Copy
H = entropy(img);
img – 2D matrix (uint8) representing the grayscale image.
Output:
H – Scalar (double) entropy value in bits.
Algorithm (Working Principle): The function builds a histogram of intensity frequencies and converts it to probabilities p(i). It then computes Shannon entropy:

[ ;H = -\sum_{i} p(i),\log_{2} p(i); ]

(summing only over p(i)>0)
. In practice, we normalize the 256-bin histogram by the total number of pixels, then compute -p*log2(p) for each bin and sum. This follows the standard information-theoretic definition
.

Example Usage:

scilab
Copy
// Create a random 100×100 image
img = grand(100,100,'uin',0,255);
H = entropy(img);
disp("Entropy = " + string(H));
Test Cases: (8-bit images, using user-provided results where available)

Test Case	Description	Expected Entropy (bits)	Interpretation
All zeros image	Uniform black	0	No variation → entropy = 0.
Constant image (e.g. all 100)	Uniform gray	0	Uniform → entropy = 0.
Half black/half white	Two equal values	≈1	Two equally likely intensities → H ≈1 bit.
Random (uniform 0–255)	Uniform noise	≈7.99	Maximal randomness for 8-bit data.
Gaussian noise (σ small)	Some randomness	~6–7	Moderate randomness depending on noise level.

Validation Notes:

If all pixels are the same, entropy = 0 (as shown).
If img is empty or non-numeric, behavior is unspecified.
Values outside [0,255] should be clamped or ignored (implementation-dependent).
Numeric stability: Use log2; skip bins where p(i)=0 to avoid log(0).
Implementation Notes:

Uses Scilab base functions (no special toolboxes).
Internally converts img to double, computes histogram (e.g. with histc), and sums -p.*log2(p).
Place entropy.sci and entropy.sce in the same directory; include this README.txt alongside.
