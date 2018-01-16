---
layout: post
title:  "- How computers learn - <br/> Part 1: Linear relationships"
date:   2017-11-04 01:00:00
categories: Statistics
image:
  feature: linear.jpeg
  topPosition: 0px
syntaxHighlighter: language-python
---

<p align="justify">
In this series of blog posts I want to explore how computers can learn. 
</p>

<p align="justify">
Suppose we want a computer to learn the relationship between two things. For example (off the top of my head) how much water a watermelon plant needs to grow one centimetre in a day (disclaimer: I'm no expert on watermelons, but I'm going to make up some numbers here anyway). Lets say that for every cup of water we give the plant will grow 2cm in a day, then we can express this relationship as follows    

$$y = 2x$$

where $y$ is the variable output of growth in centimetres given the input $x$, <i>i.e.</i> the number of cups of water. This relationship is linear, in other words the more water we give the more growth we get <i>ad infinitum</i> (which I guess is fairly unrealistic, but lets work with this for now). 
</p>

<br>

```python
# import required modules
import numpy as np

# generate data with relationship y = 2x
x = np.arange(0, 10, 1)
y = 2*x
```

<p align="justify">

Here we have expressed $y$ as a function of $x$, which we typically write as $y = f(x)$. For watermelons $f(x) = 2x$, but for potatoes $f$ could perhaps be entirely different, such as $3x/4$. To distinguish the two, we could define a new function $g$ for potatoes, such that $g(x) = 3x/4$.

</p>

<br>

```python
# import required modules
import matplotlib.pyplot as plt

# define function for potatoes
g = 3*x/4

# plot relationships
plt.scatter(x, y, label='Watermelon')
plt.scatter(x, g, label='Potato')
plt.ylabel('Growth (cm / per day)')
plt.xlabel('Water (cups)')
plt.legend()
plt.show()
```

<div class="img img--fullContainer img--16xLeading" style="background-image: url({{ site.baseurl_posts_img }}watermelonsPlot.png);"></div>

<p>

In this hypothetical scenario, the figure above shows the rate of growth for watermelons versus potatoes. Watermelons are seen to grow much faster given the same amount of water per day. 

</p>

<p>

Will a computer be able to learn this distinction? Or any relationship at all? In the next post, we will inject some more realism into the above picture and look at observational noise and the normal distribution.

</p>

<hr>

<p>
A python notebook version of this post can be found <a href="https://github.com/arnupretorius/blog/blob/master/How%20computers%20learn/1_linear%20_relationships/17_11_04_linear_relationships.ipynb" style="text-decoration: none; border-bottom: 1px solid #ff0000; color: #000000;">here</a>.
</p>

