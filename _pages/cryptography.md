---
permalink: /cryptography/
title: "Cryptography"
excerpt: ""
header:
  overlay_image: projects.JPG
  overlay_filter: rgba(51, 51, 90, 0.75)
author_profile: false
og_image: og_image.png
---
<script src="https://sagecell.sagemath.org/static/embedded_sagecell.js"></script>
<script>
sagecell.makeSagecell({inputLocation: '.sageread',
					   template:	  sagecell.templates.restricted});
sagecell.makeSagecell({inputLocation: '.sage'});
</script>
<link rel="stylesheet" type="text/css" href="https://discovermaths.uk/files/sagecell_embed.css">

## Encoding and Decoding

In order to use any of the encryption techniques we looked at in the workshop, we first needed to *encode* our plaintext message from letters into numbers. This is the basic encoding we used in the workshops:

<figure>
	<a href="/images/encoding-table-1.png"><img src="/images/encoding-table-1.png"></a>
</figure>
<figure>
	<a href="encoding-table-2.png"><img src="/images/encoding-table-2.png"></a>
</figure>

**Example:** If we wanted to encode the word "hello", for example, we would do so by replacing the letters by their corresponding numbers in the table above:
{: .notice}

| **H** | **E** | **L** | **L** | **O** |
|:-:|:-:|:-:|:-:|:-:|
| 7 | 4 | 11 | 11 | 14 |

So the plaintext "hello" is encoded to 7 4 11 11 14.
{: .notice}

## Encrypting and Decrypting

In the workshop, we looked at a few different methods of encryption and their respective methods of decryption. Here's a reminder of the ones we looked at and their methods:

### Caesar Shift Ciphers

Caesar Shift Ciphers are named after Julius Caesar, the Roman emperor, who encrypted secret messages to his army generals in this way. This is how it's done:

1. Convert your message into numbers (encode).
2. Choose a key number.
3. Add the key number to each number (shift).
4. Reduce the numbers modulo 26.
5. Convert your message back to letters (decode).

**Example:** If we choose the key number to be 15 and want to encrypt the plaintext "hello" using a Caesar Shift Cipher, it would work like this:
{: .notice}

|                | H   | E   | L   | L   | O   |
|:-:             |:-:  |:-:  |:-:  |:-:  |:-:  |
| **Encoded**    | 7   | 4   | 11  | 11  | 14  |
| **Key**        | +15 | +15 | +15 | +15 | +15 |
| **Encrypted**  | 22  | 19  | 26  | 26  | 29  |
| **Mod 26**     | 22  | 19  | 0   | 0   | 3   |
| **Ciphertext** | W   | T   | A   | A   | D   |

So the plaintext "hello" is encrypted to the ciphertext "wtaad".
{: .notice}

If you know what they encryption key was, you just work backwards to decrypt (encode the ciphertext, subtract the key, reduce modulo 26, and then decode). If you *don't* know the shift key, you might need to use a bit of [frequency analysis](https://crypto.interactive-maths.com/frequency-analysis-breaking-the-code.html) or knowledge of common word endings, letter combinations or short words within the language you're working in to figure out the key.

### Affine Ciphers

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

So the plaintext "hello" is encrypted to the ciphertext "xojjs".
{: .notice}

Decrypting affine ciphers is more complex. We're used to being able to find inverses of functions quite easily by working backwards and applying the inverses of each individual operation in the function in reverse BIDMAS order. Using our prior knowledge of functions, we could find the inverse of the function $3x+2$ to be $\frac{1}{3}(x-2)$. 

Unfortunately when working Modulo 26 (or Modulo anything for that matter), fractions don't exist -- we only have the integers from 0 to 25 (or 0 to $n-1$ for Mod $n$). With this, we need to find the *multiplicative inverse* of 3 mod 26 in order to find the decrypying function; that is, the number we can multiply by 3 to get 1 mod 26. This can be found quite easily, as $3*9=27\equiv1\text{ mod }26$. This means that the inverse function would actually be $9(x-2)$ or $9x-18$ if we expand it.

**Example:** We can work backwards from the ciphertext we found above to check this is correct.
{: .notice}

|                      | X   | O   | J   | J   | S   |
|:-:                   |:-:  |:-:  |:-:  |:-:  |:-:  |
| **Encoded ($x$)**    | 23  | 14  | 9   | 9   | 18  |
| **$9x$**             | 207  | 126  | 81  | 81  | 162  |
| **$-18$**             | 189  | 108  | 63  | 63  | 144  |
| **Mod 26**           | 7   | 4   | 11  | 11  | 14  |
| **Plaintext**        | H   | E   | L   | L   | O   |

So the decrpyion key which corresponds to the encryption $3x+2$ is $9x-18$.
{: .notice}

Not all affine ciphers are valid for encryption, as not all numbers are invertible (or reducible) mod 26. Only numbers which have no common factors with 26 have inverses and so whilst the $b$ in $ax+b$ can be anything, the $a$ must only be invertible / reducible mod 26 when working with a basic 26-letter alphabet (i.e. working mod 26).

The following SageMath code computes the inverses of each of the invertible / reducible numbers mod 26.

<div class="sageread">
	<pre><script type="text/x-sage">
for i in Zmod(26).list_of_elements_of_multiplicative_group():
    x = inverse_mod(i,26)
    print("Inverse of", i, "is", x)
	</script></pre>
</div>

<br>
The reason we can't use a non-invertible / irreducible number for $a$ in an affine cipher can be seen when we try the affine cipher $2x$. If we encrypt the encoded alphabet (numbers 0-25), we get the ciphertext alphabet which is shown by the following SageMath code:

<div class="sage">
	<pre><script type="text/x-sage">
for i in range(26):
	x = (2 * i) % 26
	print(i, "mod 26 =", x)
	</script></pre>
</div>

<br>
You'll notice that the ciphertext alphabet begins to repeat itself halfway through, which means that if the letters *a* and *n* both encrypt to *a*, so it would be impossible to decrypt a message encoded by this affine cipher or any affine cipher which uses a non-invertible.

Have a play around with the code above and chance the 2 to any other non-invertible number modulo 26 (2, 4, 6, 8, 10, 12, 13, 14, 16, 18, 20, 22, 24, or 26) and you'll see a similar outcome of a repeated alphabet.

### Vigenère Cipher

For a long time, the Vigenère Cipher was regarded to be unbreakable. It's very simple to encrypt something using this cipher, but unless you know the key, it's very difficult to decrypt. The Vigenère Cipher works as follows:

1. Choose a password and encode it.
2. Convert your message into numbers (encode).
3. Shift the $n^{th}$ letter of your encoded plaintext by the value of the $n^{th}$ letter in the password (shift).
4. Continue on until you reach the end of your password.
5. Move back to the start of your password and shift the next letter of your encoded plaintext by the value of the first letter in the password (shift).
6. Repeat steps 4 and 5 until your message has been encrypted.
7. Reduce the numbers modulo 26.
8. Convert your message back to letters (decode).

**Example:** If we choose the password to be "code" and want to encrypt the plaintext "Message" using a Caesar Shift Cipher, we would first encode our password:
{: .notice}

|                | C   | O   | D   | E   |
|:-:             |:-:  |:-:  |:-:  |:-:  |
| **Encoded**    | 2   | 14  | 3   | 4   |

This tells us how much to shift each letter of our message by when encrypting. The encryption works like this:
{: .notice}

|                | M   | E   | S   | S   | A   | G   | E   |
|:-:             |:-:  |:-:  |:-:  |:-:  |:-:  |:-:  |:-:  |
| **Encoded**    | 12  | 4   | 18  | 18  | 0   | 6   | 4   |
| **Password**   | C   | O   | D   | E   | C   | O   | D   |
| **Shift**      | +2  | +14 | +3  | +4  | +2  | +14 | +3  |
| **Encrypted**  | 14  | 18  | 21  | 22  | 2   | 20  | 7   |
| **Mod 26**     | 14  | 18  | 21  | 22  | 2   | 20  | 7   |
| **Ciphertext** | O   | S   | V   | W   | C   | U   | H   |

So the plaintext "message" is encrypted to the ciphertext "osvwcuh".
{: .notice}

### Public Key Cryptography: RSA