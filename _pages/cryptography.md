---
permalink: /cryptography/
title: "Cryptography"
excerpt: ""
header:
  overlay_image: downloads.JPG
  overlay_filter: rgba(51, 51, 90, 0.75)
author_profile: true
og_image: og_image.png
---
<script src="https://sagecell.sagemath.org/static/embedded_sagecell.js"></script>
    <script>
    // Make the div with id 'mycell' a Sage cell
    sagecell.makeSagecell({inputLocation:  '#mycell',
                           template:       sagecell.templates.minimal,
                           evalButtonText: 'Evaluate'});
    </script>
	
## SageMath Cell
<div id="mycell"><script type="text/x-sage">
  for i in range(26):
    x = (2 * i) % 26
    print(x)
</script></div>
