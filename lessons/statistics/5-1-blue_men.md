[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

**Exercise 1**   In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters µ = 178 cm and σ = 7.7 cm for men, and µ = 163 cm and σ = 7.3 cm for women.
In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf.

```python
height_min = (5 * 12 + 10) * 2.54
height_max = (6 * 12 + 1) * 2.54
mean = 178
sigma = 7.7

percentage = (scipy.stats.norm.cdf(height_max, loc = mean, scale = sigma) -
              scipy.stats.norm.cdf(height_min, loc = mean, scale = sigma)) * 100

print("{0:0.1F}% of the U.S. male population is in the Blue Man range".format(percentage))
```
**34.3%** of the U.S. male population is in the height range for the Blue Man Group.
