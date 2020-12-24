[Think Stats Chapter 9 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2010.html#toc90) (resampling)

**Exercise 2**  In Section 9.3, we simulated the null hypothesis by permutation; that is, we treated the observed values as if they represented the entire population, and randomly assigned the members of the population to the two groups.

An alternative is to use the sample to estimate the distribution for the population, then draw a random sample from that distribution. This process is called resampling. There are several ways to implement resampling, but one of the simplest is to draw a sample with replacement from the observed values, as in Section 9.10.

Write a class named DiffMeansResample that inherits from DiffMeansPermute and overrides RunModel to implement resampling, rather than permutation.

Use this model to test the differences in pregnancy length and birth weight. How much does the model affect the results?

```python
import first
import hypothesis
import numpy as np

class DiffMeansResample(hypothesis.DiffMeansPermute):
    def RunModel(self):
        group1 = np.random.choice(self.pool, self.n, replace = True)
        group2 = np.random.choice(self.pool, self.m, replace = True)
        data = group1, group2
        return data
        
live, firsts, others = first.MakeFrames()
prglngths = firsts.prglngth.values, others.prglngth.values
ht_prglngths = DiffMeansResample(prglngths)
pval_prglngths = ht_prglngths.PValue()
pval_prglngths

birthwgts = firsts.totalwgt_lb.values, others.totalwgt_lb.values
ht_birthwgts = DiffMeansResample(birthwgts)
pval_birthwgts = ht_birthwgts.PValue()
pval_birthwgts
```
