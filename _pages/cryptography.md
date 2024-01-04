---
permalink: /cryptography/
title: "Cryptography"
excerpt: ""
header:
  overlay_image: projects.JPG
  overlay_filter: rgba(51, 51, 90, 0.75)
author_profile: false
og_image: og_image.png
toc: true
---
<script src="https://sagecell.sagemath.org/static/embedded_sagecell.js"></script>
<script>
sagecell.makeSagecell({inputLocation: '.sage',
					   template:	  sagecell.templates.restricted});
</script>
<link rel="stylesheet" type="text/css" href="https://discovermaths.uk/files/sagecell_embed.css">

# Encoding and Decoding

In order to use any of the encryption techniques we looked at in the workshop, we first needed to *encode* our plaintext message from letters into numbers. This is the basic encoding we used in the workshops:

||||||||||||||
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **A** | **B** | **C** | **D** | **E** | **F** | **G** | **H** | **I** | **J** | **K** | **L** | **M** |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
| **N** | **O** | **P** | **Q** | **R** | **S** | **T** | **U** | **V** | **W** | **X** | **Y** | **Z** |
| 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 |

**Example:** If we wanted to encode the word "hello", for example, we would do so by replacing the letters by their corresponding numbers in the table above:
{: .notice}

| **H** | **E** | **L** | **L** | **O** |
|:-:|:-:|:-:|:-:|:-:|
| 7 | 4 | 11 | 11 | 14 |

So the word "hello" is encoded to 7 4 11 11 14.
{: .notice}

# Encrypting and Decrypting

In the workshop, we looked at a few different methods of encryption and their respective methods of decryption. Here's a reminder of the ones we looked at and their methods:

## Caesar Shift Ciphers

Caesar Shift Ciphers are named after Julius Caesar, the Roman emperor, who encrypted secret messages to his army generals in this way. This is how it's done:

1. Convert your message into numbers (encode).
2. Choose a key number.
3. Add the key number to each number (shift).
4. Convert your message back to letters (decode).

**Example:** If we choose the key number to be 15 and want to encrypt the plaintext "hello" using a Caesar Shift Cipher, it would work like this:
{: .notice}

|                | H   | E   | L   | L   | O   |
|:-:             |:-:  |:-:  |:-:  |:-:  |:-:  |
| **Encoded**    | 7   | 4   | 11  | 11  | 14  |
| **Key**        | +15 | +15 | +15 | +15 | +15 |
| **Encrypted**  | 22  | 19  | 26  | 26  | 29  |
| **Mod 26**     | 22  | 19  | 0   | 0   | 3   |
| **Ciphertext** | W   | T   | A   | A   | D   |

So "hello" would encrypt to the ciphertext "wtaad".
{: .notice}

If you know what they encryption key was, you just work backwards to decrypt (encode the ciphertext, subtract the key, reduce modulo 26, and then decode). If you *don't* know the shift key, you might need to use a bit of [frequency analysis](https://crypto.interactive-maths.com/frequency-analysis-breaking-the-code.html) or knowledge of common word endings, letter combinations or short words within the language you're working in to figure out the key.

## Affine Ciphers

An affine cipher is like a Caesar shift cipher, but with an added layer of complexity. Instead of shifting everything by a constant value, we shift by an *affine* function in the form $ax+b$.

**Example:** If we encrypt the plaintext "hello" using the affine function $3x+2$, it would work like this:
{: .notice}

|                      | H   | E   | L   | L   | O   |
|:-:                   |:-:  |:-:  |:-:  |:-:  |:-:  |
| **Encoded ($x$)**    | 7   | 4   | 11  | 11  | 14  |
| **$3x$**             | 21  | 12  | 33  | 33  | 42  |
| **$+2$**             | 23  | 14  | 35  | 35  | 44  |
| **Mod 26**           | 23  | 14  | 9   | 9   | 18  |
| **Ciphertext**       | X   | O   | J   | J   | S   |

So "hello" would encrypt to the ciphertext "xojjs".
{: .notice}

This is a test of embedding SageMathCell to a webpage!

<div class="sage">
	<pre><script type="text/x-sage">
for i in range(26):
	x = (2 * i) % 26
	print(i, "mod 26 =", x)
	</script></pre>
</div>

<div class="sage">
	<pre><script type="text/x-sage">
for i in (1,3,5,7,11,17,25):
    x = inverse_mod(i,26)
    print("Inverse of", i, "is", x)
	</script></pre>
</div>