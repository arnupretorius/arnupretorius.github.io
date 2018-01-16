---
layout: post
title:  "- How computers learn - <br/> Part 2: Noise and the normal distribution"
date:   2017-11-06 01:00:00
categories: Statistics
image:
  feature: fall-autumn-red-season.jpg
  topPosition: 0px
syntaxHighlighter: language-python
---

<p align='justify'>

In the <a href="{{ page.previous.url }}" style="text-decoration: none; border-bottom: 1px solid #ff0000; color: #000000;">previous post</a>, we looked at linear relationships and started asking the question of how a computer might be able to learn such a relationship. Specifically, we constructed a toy linear relationship between the number of cups of water represented by the variable $x$ and the number of centimetres of growth per day $y$, for a watermelon plant (the example is a bit weird I know, but I think plants are pretty cool so I will stick with this one). However, the relationship seemed fairly unrealistic. Firstly, more water always resulted in more growth and the change in growth was exactly the same for every one unit change in water.  Ultimately, if we are interested in getting computers to learn something, then we would like them to be able to learn aspects of the real world, and the real world is full of uncertainty. 

</p>

<p align='justify'>

To make our example more realistic, we are going to add <i>noise</i> to the situation. The source of the noise is unknown, however we might have a guess at various culprits such as the weather (extra rain, humidity, drought), human error (spilling water, not measuring exactly how much water we give) and a host of other reasons for the relationship to be non-deterministic. This means that the growth of a watermelon plant won't be exactly the same given the same amount of water each time round. What is fundamental about this is that we can't solely rely on specific observations (since they might change in the future), instead we have to find a way to somehow distil into the computer a <i>general</i> relationship, established from a finite sample, that seems to hold on average.

</p>

<p align='justify'>

So how can we add uncertainty to our toy example? Well, the mathematics of uncertainty is written in terms of probabilities and we can make use of <i>probability distributions</i> to represent the noise in our scenario. A probability distribution is simply a function that tells us, given that we have observed something, how likely observing <i>that</i> something really is. For example, say we plant $50$ watermelon plants for $50$ years, then by now we might have a fairly good intuition for the size of a typical watermelon, give or take. Therefore, if someone were to hand us a new watermelon (of a certain size) from our garden in the new year, we would to some extent be able to say how likely it is that a watermelon of the same size would grow again the following year. 

</p>

<center>
<blockquote class="u--startsWithDoubleQuote">A probability distribution is simply a function that tells us, given that we have observed something, how likely observing that something really is.</blockquote>
</center>


<p align="justify">

Now if the watermelon that was just handed to us was enormous, or microscopic, our intuition would've steered us to the conclusion that this was a rare event and is not likely to happened again. On the other hand, if it looked quite normal, we would say, 'sure, we will get plenty more of these next year'. This human institution isn't some fluke, but instead comes from an internal probability distribution that has been well approximated through repeated observation of the real world. 

</p>

<p align='justify'>
As it happens, there is a certain distribution that is extremely common in the natural world. It is called the <i>normal distribution</i>, also referred to as the <i>Gaussian</i> distribution (see the interactive visualisation below).
</p>

<br>

<center>
	<iframe src="https://plot.ly/~arnup/2.embed?showlink=false" seamless="seamless" scrolling="no" width="800px" height="500px"></iframe>	
</center>

<p>
The normal distribution is defined as

\begin{align}
    p(x) = \frac{1}{\sqrt{2\pi \sigma^2}}e^{-\frac{(x - \mu)^2}{2\sigma^2}},
\end{align}

where the parameters $\mu$ and $\sigma^2$ characterise the shape of the distribution. 
</p>

<br>

```python
# required imports
import numpy as np

# normal probability distribution function
def normal_distribution(x, mu, sigma):
    p_x = (1/np.sqrt(2*np.pi*sigma**2))*np.exp((-(x - mu)**2)/(2*sigma**2))
    return p_x
```

<p align="justify">

The parameter $\mu$ is the mean of the distribution and specifies the location of the peak (the most probable observation), whereas $\sigma^2$ is responsible for how often and to what extent observations vary from the mean. We usually write $x \sim \mathcal{N}(\mu, \sigma^2)$ to indicate that a random variable $x$ is distributed according to a normal distribution with mean $\mu$ and variance $\sigma^2$. The quantity $\sigma$ is referred as the standard deviation (you can play around with the standard deviation to change the shape of the distribution above).

</p>

<br>

```python
# required imports
import plotly.plotly as py
from plotly.graph_objs import *

# generate data and range of parameters
x = np.arange(-10, 10, 0.1)
sigma_range = np.arange(0.1, 5, 0.1)

# create data dictionary
data = [dict(
        visible = False,
        line=dict(width=3),
        name = 'p(x)',
        x = x,
        y = normal_distribution(x, 0, step)) for step in sigma_range]

# set starting data configuration (sigma = 1)
data[9]['visible'] = True

# for each value of sigma show corresponding data
steps = []
for i in range(len(data)):
    step = dict(
        method = 'restyle',
        label=str(sigma_range[i]),
        args = ['visible', [False] * len(data)],
    )
    step['args'][1][i] = True # Toggle i'th trace to "visible"
    steps.append(step)

# define plotly slider
sliders = [dict(
    active = 9,
    currentvalue = {"prefix": 'Standard deviation: '},
    pad = {"t": 50},
    len = 0.7,
    steps = steps
)]

# create layout and plot
layout = dict(sliders=sliders, xaxis={'title':'x'}, yaxis={'title':'p(x)'})
fig = dict(data=data, layout=layout)
py.iplot(fig, filename = 'normal-dist')
```

<p align="justify">
	
The normal distribution is crucial for many aspects of learning and the assumption that the observed data comes from a normal distribution is regularly made in practice. In the next post we will use the normal distribution to sample noise and generate more realistic observations.  

</p>

<hr>

<p>
A python notebook version of this post can be found <a href="https://github.com/arnupretorius/blog/blob/master/How%20computers%20learn/2_noise_and_normal_distribution/17_11_09_noise_and_normal_distribution.ipynb" style="text-decoration: none; border-bottom: 1px solid #ff0000; color: #000000;">here</a>.
</p>

