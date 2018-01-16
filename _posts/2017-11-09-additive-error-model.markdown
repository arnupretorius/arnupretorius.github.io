---
layout: post
title:  "- How computers learn - <br/> Part 3: The additive error model"
date:   2017-11-06 01:00:00
categories: Statistics
image:
  feature: black-and-white-trees-winter-branches.jpg
  topPosition: 0px
syntaxHighlighter: language-python
---

# This is a header

<p align='justify'>

</p>

<p align='justify'>

</p>

<p align='justify'>

</p>

<center>
<blockquote class="u--startsWithDoubleQuote">A probability distribution is simply a function that tells us, given that we have observed something, how likely observing that something really is.</blockquote>
</center>


<p align="justify">

</p>

<br>

<center>
	<div class="img img--fullContainer img--16xLeading" style="background-image: url({{ site.baseurl_posts_img }}noise.gif);"></div>
</center>

```python
# required imports
import numpy as np

# normal probability distribution function
def normal_distribution(x, mu, sigma):
    p_x = (1/np.sqrt(2*np.pi*sigma**2))*np.exp((-(x - mu)**2)/(2*sigma**2))
    return p_x
```


