[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

**Exercise 4**   Using the variable *totalwgt_lb*, investigate whether first babies are lighter or heavier than others. Compute Cohen’s d to quantify the difference between the groups. How does it compare to the difference in pregnancy length?

```python
import math
def cohen_d(firsts, others):
    diff = firsts.mean() - others.mean()

    var1 = firsts.var()
    var2 = others.var()
    n1, n2 = len(firsts), len(others)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / math.sqrt(pooled_var)
    return d
    
prglngth_cd = cohen_d(firsts.prglngth, others.prglngth)
print("Cohen's d for pregnancy length is {0:.3f}".format(prglngth_cd))

totalwgt_cd = cohen_d(firsts.totalwgt_lb, others.totalwgt_lb)
print("Cohen's d for birth weight is {0:.3f}".format(totalwgt_cd))
```
**Cohen's d for birth weight is -0.089.**
**Cohen's d for pregnancy length is 0.029.**
