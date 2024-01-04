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
<script>sagecell.makeSagecell({"inputLocation": ".sage"});</script>

This is a test of embedding SageMathCell to a webpage!

<div class="sage">{hide: [fullScreen]}
	<script type="text/x-sage" id="mycode">
for i in range(26):
	x = (2 * i) % 26
	print(x)
	</script>
</div>