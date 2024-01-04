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

| <div style="width:7.6923%">A</div> | <div style="width:7.6923%">B</div> | <div style="width:7.6923%">C</div> | <div style="width:7.6923%">D</div> | <div style="width:7.6923%">E</div> | <div style="width:7.6923%">F</div> | <div style="width:7.6923%">G</div> | <div style="width:7.6923%">H</div> | <div style="width:7.6923%">I</div> | <div style="width:7.6923%">J</div> | <div style="width:7.6923%">K</div> | <div style="width:7.6923%">L</div> | <div style="width:7.6923%">M</div> | 
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |

| <div style="width:7.6923%">N</div> | <div style="width:7.6923%">O</div> | <div style="width:7.6923%">P</div> | <div style="width:7.6923%">Q</div> | <div style="width:7.6923%">R</div> | <div style="width:7.6923%">S</div> | <div style="width:7.6923%">T</div> | <div style="width:7.6923%">U</div> | <div style="width:7.6923%">V</div> | <div style="width:7.6923%">W</div> | <div style="width:7.6923%">X</div> | <div style="width:7.6923%">Y</div> | <div style="width:7.6923%">Z</div> |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 |

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